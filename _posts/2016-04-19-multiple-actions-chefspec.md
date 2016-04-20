---
layout: post
title: Testing multiple actions in ChefSpec
summary: Order matters!
---
## Problem

I was testing a resource that was parameterized with multiple actions when I stumbled upon an issue. There isn't a way to test the order of multiple actions on one resource.

Here's an example of multiple actions called on the same resource, based off of [ChefSpec examples](https://github.com/sethvargo/chefspec/):

```ruby
service 'resource' do
  action [:enable, :start]
end
```

```ruby
describe 'multiple_actions::default' do
  let(:chef_run) { ChefSpec::SoloRunner.converge(described_recipe) }

  it 'executes both actions' do
    expect(chef_run).to enable_service('resource')
    expect(chef_run).to start_service('resource')
  end
end
```

We can assert that `:enable` and `:start` were called individually, but we cannot assert that `:enable` was called before `:start`. This is unfortunate because we should treat the action list as an atomic unit. Let's say, in this example, we don't want to start a service if we can't enable it on boot; there is no way to test that dependency between actions.

## Possible solution

`ChefSpec::Matchers::ResourceMatcher`'s [`initialize`](https://github.com/sethvargo/chefspec/blob/master/lib/chefspec/matchers/resource_matcher.rb#L6-L10) would expect an array of actions or a single action.

```ruby
def initialize(resource_name, expected_action, expected_identity)
  @resource_name     = resource_name
  @expected_action   = expected_action
  @expected_identity = expected_identity
end
```

The overriden `Chef::Resource`'s [`performed_action?`](https://github.com/sethvargo/chefspec/blob/master/lib/chefspec/extensions/chef/resource.rb#L42-L44) would expect an array of actions or a single action in `ChefSpec::Matchers::ResourceMatcher`'s [`matches?`](https://github.com/sethvargo/chefspec/blob/master/lib/chefspec/matchers/resource_matcher.rb#L45-L54).

```ruby
def matches?(runner)
  @runner = runner

  if resource
    ChefSpec::Coverage.cover!(resource)
    resource.performed_action?(@expected_action) && unmatched_parameters.empty? && correct_phase?
  else
    false
  end
end
```

`Chef::Resources`'s [`@performed_actions`](https://github.com/sethvargo/chefspec/blob/master/lib/chefspec/extensions/chef/resource.rb#L6) would become an ordered hash, or `Chef::Resource` would keep track of ordering in some other way. `performed_action?` would then account for the ordering of the actions.

```ruby
def performed_action(action)
  @performed_actions[action.to_sym]
end

def performed_action?(action)
  !!performed_action(action)
end
```

Currently, `ChefSpec` doesn't support dynamically generated matchers, so we'd roll our own to support testing multiple actions.

```ruby
def enable_and_start_service(resource_name)
  ChefSpec::Matchers::ResourceMatcher.new(:service, [:enable, :start], resource_name)
end
```
