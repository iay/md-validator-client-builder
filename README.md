# Metadata Validator Web Service Client Builder

This project automates building of the client libraries
for the `md-validator` micro-service.

To perform a simple build:

```bash
$ mvn clean compile
```

For now, this only builds the source for a Ruby gem called
`md-validator-client`. In principle, we could add additional executions for
libraries in other languages.

The generated code will appear in `target/md-validator-client-ruby`, which is
also the name of the repository the code gets pushed to.

## Pushing Generated Source to a Repository

This is not as trivial a process as you might hope, because of the way that the
code is re-generated in full every time. To simplify this process, there's a
`prep-ruby` script which does some of the repository setup. The generated
repository also has a `git_push.sh`, but it only handles public `github.com`
repositories.

```bash
$ mvn clean
$ ./prep-ruby
$ mvn compile
$ cd target/md-validator-client-ruby
$ git add --all .
$ git commit -m "This is what is new"
$ git push --set-upstream origin main
```

## Build and Publish the Gem

The gem is built and published to
[RubyGems.org](https://rubygems.org) as follows:

```bash
$ gem build md-validator-client.gemspec
$ gem push md-validator-client-*.gem
```
