# Ruby Style Guide

## Table of Contents
- [Ruby Style Guide](#ruby-style-guide)
  * [Table of Contents](#table-of-contents)
  * [Ruby Style Guide and Best Practices](#ruby-style-guide-and-best-practices)
  * [Style Baseline](#style-baseline)
  * [Design Baseline](#design-baseline)
  * [Testing](#testing)
  * [Further Reading](#further-reading)


## Ruby Style Guide and Best Practices

This document serves as a style and best practices guide for Conjur contributors who are writing
Ruby source code. The purpose of this guide is to provide common conventions and to describe some
common pitfalls to avoid, so that our code base is consistent, readable, and maintainable across
various projects.

Much of the content for this style guide is drawn from publicly available Ruby style guides.

This guide is intended to be a "living document" in the sense that it's expected that it will evolve
as we refine and hone our Ruby knowledge base.

## Style Baseline
- Follow this official guidelines of the Ruby language https://docs.ruby-lang.org/en/master/doc/syntax/methods_rdoc.html
  
- Methods whose purpose is to produce a side effect (change a file, make a network call, raise an error, etc) should have verb phrase names. 

  ```ruby
  def call
    validate_and_decode_token
    get_jwt_identity_from_request
    validate_host_has_access_to_webservice
    validate_origin
    validate_restrictions
    audit_success
    new_token
  rescue => e
    audit_failure(e)
    raise e
  end
  ```

  

- Methods that return an object should have the name of the returned object so these functions should not have verb phrase names.
   In some cases, these rules may conflict when a side-effectful method also returns a value. Here the "verb phrase" rule should win since indicating the side effect is more important.

- For low-level style decisions about formatting, etc, we follow the ruby style. We advice to use rubocop to auto correct offence in the files you change before submitting to PR.

- Avoid "name stutter". That is, don't repeat a name from the module path in a class, and don't repeat a name from the class in a method. For example:

   ```ruby
   # bad
   class MyCar
     def start_car_engine
       # ...
     end
   end
   
   # good
   class MyCar
     def start_engine
       # ...
     end
   end
   
   # bad
   module Authenticators
     class OktaAuthenticator
       #...
     end
   end
   
   # good
   module Authenticators
     class Okta
       #...
     end
   end
   ```

- In constuctor of classes separate input handling and dependency handling with empty line

- In command class implement methods in the order they are called

  ```ruby
  def call
    func_a
    func_b
    func_c
  end
  
  private
  
  def func_a
    # ...
  end
  
  def func_b
    # ...
  end
  
  def sub_func_b
    # ...
  end
  
  def func_c
    # ...
  end
  ```

- In functions with many parameters put each parameter in seperate line in the declaration. In this case end each param with ":" so the caller will need to specify name of variable for each param.

  ```
  def method(param1:, param2:, param3:)
  
  # is preferable to put each arguemnt in its own line
  
    def method(
      param1:
      param2:
      param3:
    )
  
  # since it fits comfortably on one line.
  ```


## Design Baseline

- On any new class ask yourself if it should be a class or command class. Command Classes coordinate the execution of a multi-step process.

  https://github.com/cyberark/conjur/blob/master/app/domain/README.md#the-functional-object-oriented-style

- No need for interface classes. Ruby is duck typed, so if you need to define an interface, try handling it with tests.

- *Never* use inheritance or mixins.

- Dependencies for classes should be passed in the constructor. Try to avoid putting classes as dependencies if its possible and pass only instances.

  ```ruby
  def initialize(
    authenticator_input:,
    logger: Rails.logger,
    extract_token_from_credentials: Authentication::AuthnJwt::InputValidation::ExtractTokenFromCredentials.new,
    create_identity_provider: Authentication::AuthnJwt::IdentityProviders::CreateIdentityProvider.new
  )
  ```
  
- Use memoization when you need to run an "expensive operation" more than onceand are sure that it's safe to cache the output (DB queries, API requests, etc..). Use the '||=' construct -- this is the idiomatic pattern for memoization in ruby. Unless there is a naming conflict, name your instance variable (eg, `@my_method`) after your method (eg, `my_method`).

  ```ruby
  def identity_role
    @identity_role ||= @role_class.by_login(
      jwt_identity,
      account: account
    )
  end
  ```

- For the special case when the value being memoized is boolean, the above method won't work. That's because both `nil` and `false` evaluate to false, so the `||=` pattern can't distinguish between an uninitialized value and and already initialized value that happens to be `false`. For this case we suggest the following explicit check:

  ```ruby
  def identity_available?
    return @identity_available if [true, false].include?(@identity_available)
  
    @identity_available = username_exists?
  end
  ```

- A command class should never call new on anything besides a value object. If it needs to do that, the “already -new’d” thing should have been passed in to begin with.  Related to this: value object classes are not dependencies and can be referred to directly. So they will never need to be passed in.

  ```ruby
  Authenticator = CommandClass.new(
        dependencies: {
          token_factory: TokenFactory.new, # Non value object so instance passed
          logger: Rails.logger, # Non value object so instance passed
          audit_log: ::Audit.logger, # Non value object so instance passed
          validate_origin: ::Authentication::ValidateOrigin.new, # Non value object so instance passed
          validate_role_can_access_webservice: ::Authentication::Security::ValidateRoleCanAccessWebservice.new, # Non value object so instance passed
          role_class: ::Role, # Value object so class can be passed
          webservice_class: ::Authentication::Webservice,# Value object so class can be passed
          role_id_class: Audit::Event::Authn::RoleId # Value object so class can be passed
        },
        inputs: %i[vendor_configuration authenticator_input]
      ) do
  ```

## Testing
- **rspec guidelines** ([Better Specs](http://www.betterspecs.org/)) - Best practices for developing
  with rspec

## Further Reading
- **Newsletter** ([Ruby Weekly](http://rubyweekly.com/)) - Once-weekly round-up of Ruby News and
  Articles 
- **Learning Ruby** ([The Hard Way](https://learnrubythehardway.org/book/)) - A simple book meant to
  get you started in programming with Ruby
- **Command Class** ([Github Public Page](https://github.com/jonahx/command_class)) - Read more about CommandClass design pattern implementations
   that frequently used in Conjur.
- [**Functional Architecture for the Practical Rubyist **](https://www.youtube.com/watch?v=7qnsRejCyEQ&t=1387s) - Youtube lecture provides more context for ideas above.
