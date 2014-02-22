# Rack::Spec
Define specifications of your Rack application.

## Installation
```
gem install rack-spec
```

## Usage
```ruby
require "rack"
require "rack/spec"
require "yaml"

use Rack::Spec, spec: YAML.load_file("spec.yml")

run ->(env) do
  [200, {}, ["OK"]]
end
```

```yaml
# spec.yml
meta:
  baseUri: http://api.example.com/

endpoints:
  /recipes:
    GET:
      parameters:
        page:
          type: integer
          minimum: 1
          maximum: 10
        private:
          type: boolean
        rank:
          type: float
        time:
          type: iso8601
        kind:
          type: string
          only:
            - mono
            - di
            - tri
    POST:
      parameters:
        title:
          type: string
          minimumLength: 3
          maximumLength: 10
```

## Development
```sh
# setup
git clone git@github.com:r7kamura/rack-spec.git
cd rack-spec
bundle install

# testing
bundle exec rspec
```
