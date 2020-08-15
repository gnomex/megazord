# Megazord
    Powerful rangers to rescue you with Mechanize!

The ideia is a configurable mechanized module, where you just need to configure and ask you want, instead of code and handle corner cases

* Rate Throttling
* Strategys do handle 404, 429, Errno::ECONNRESET, Net::HTTP::Persistent::Error, Net::ReadTimeout, etc
* Retryable and timeoutable
* Configurable rescue handlers
* Add extra headers when required (API)
* URL Switcher (same resource through different URLs)
* CAPTCHA avoider
* Downgrade SSL (misconfigured servers or BR org servers)
* Measurement: count reqs by url with some kind of aggregation, some configurable way to sync that data
* Loggable
*

## TODO

- [ ] act_as_robotiable
- [ ] act_as_url_switchable
- [ ] retryable
- [ ] act_as_authenticable_api
- [ ] 429_preventable


# Links

> There are some resources to learn about

- https://pragprog.com/titles/ppmetr2/metaprogramming-ruby-2/
- https://libraries.io/github/ankane/the-ultimate-guide-to-ruby-timeouts
- https://schneems.com/2020/07/08/a-fast-car-needs-good-brakes-how-we-added-client-rate-throttling-to-the-platform-api-gem/
- https://schneems.com/2020/06/25/rate-limiting-rate-throttling-and-how-they-work-together/
- https://cloud.google.com/solutions/rate-limiting-strategies-techniques#techniques-enforcing-rate-limits
- https://medium.com/@c.andrewlong/ruby-mechanize-5-common-errors-and-how-to-fix-them-68fa88a282ec

--

# Designing the API

> still a wip

```ruby
class Robot
  include Megazord

  act_as_robotiable :loggable, :no_ssl, :accountable, :throttleable

  base_url ""
  retryable strategy: :backpressure
  prevent :captcha, rate: 10, per: :hour
  prevent :429
  url_switchable [] # urls
  authenticable  {} #extra headers
  handleable_with [
    { "ex_class1": lambda {|e| puts e.message }},
    { "ex_class2": lambda {|e| puts "#{e.message} again" }},
  ] # custom handlers


end


```
