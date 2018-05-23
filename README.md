# inc-validator-client-builder

This project automates building of the client libraries
for the `inc-validator` micro-service.

To perform a simple build:

```bash
$ mvn clean compile
```

For now, this only builds the source for a Ruby gem called
`inc-validator-client`. In principle, we could add additional executions for
libraries in other languages.

The generated code will appear in `target/inc-validator-client-ruby`, which is
also the name of the GitLab repository the code gets pushed to.

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
$ cd target/inc-validator-client-ruby
$ git add --all .
$ git commit -m "This is what is new"
$ git push --set-upstream origin master
```

## Build and Publish the Gem

Although I don't advise it, you _could_ build the gem and publish it to
[RubyGems.org](https://rubygems.org) as follows:

```bash
$ gem build inc-validator-client.gemspec
$ gem push inc-validator-client-*.gem
```

I think this is probably less than a great idea because the rest of the world
has no particular interest in generated API client libraries for an internal
service. It's probably better to access the gem sources directly from its
remote repository, or from a cloned copy of that.
