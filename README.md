# Fluent::Plugin::Insight
Forward logs to Insight, using token based input.

Using Insight REST API gets log tokens by logset id and matches the given `log_name` to determine to which log send the messages.

## Installation
You have to build the Gem starting with this repository
install with gem or fluent-gem command as:
```sh
bundle install --path vendor/bundle
gem build fluent-plugin-insight.gemspec 
gem install fluent-plugin-insight-0.0.6.gem
```
## Usage

```
<match pattern>
    type insight
    tags hostname,environment,application
    prefix %{hostname} %{environment}-%{application}
    log_name production
    api_key test
    logset_id xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
    region eu
</match>
```

## Parameters

### type (required)
The value must be `insight`.

### logset_id (required)
InsightOPS logset id.

### region (required)
InsightOPS region (`eu` or `us`).

### log_name
Log name, used also to retrieve the correct Token to use. Default is `default`.

### tags
List of record keys which can be retrieved from record to build a log record prefix.

### prefix
Prefix is added to every log record. It's a format string which uses `tags` values.

### protocol
The default is `tcp`.

### use_json
Enables the use of json as log format, otherwise the message is retrieved by the "message" field of the record. The default is `false`.

### use_ssl
Enable/disable SSL for data transfers between Fluentd and Insight. The default is `true`.

### port
Only in case you don't use SSL, the value must be `80`, `514`, or `10000`. The default is `20000` (SSL)

### max_retries
Number of retries on failure.

## Contributing

1. Fork it ( http://github.com/Kavuti/fluent-plugin-insight/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## MIT
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
