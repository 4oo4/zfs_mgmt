# ZfsMgmt

Welcome to your new gem! In this directory, you'll find the files you need to be able to package up your Ruby library into a gem. Put your Ruby code in the file `lib/zfs_mgmt`. To experiment with that code, run `bin/console` for an interactive prompt.

TODO: Delete this and the text above, and describe your gem

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'zfs_mgmt'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install zfs_mgmt

## Usage

TODO: Write usage instructions here

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/zfs_mgmt.

## zfs user properties

zfsmgmt:weekly: integer n weekly snapshots to keep
zfsmgmt:daily: integer n daily snapshots to keep
zfsmgmt:hourly: integer n hour snapshots to keep
zfsmgmt:minage: integer seconds, minimum age of a snapshot before it will be considered for deletion
zfsmgmt:monthly: integer n montly snapshots to keep
zfsmgmt:yearly: integer n yearly backups
zfsmgmt:manage: true/false (only manage snapshots if literal string 'true', all other values are false

## Philosophy of Operation

### Timestamps in snapshot names and logging
Timestamps should use localtime. If the user wants gmt/utc they should set the system time apropriately.  (zfs uses local time in the creation property so using anything else just creates apparent mismatches.)

### Snapshot Management / zfs destroy
When destroying snapshots according to a given policy, all snapshots should be considered for deletion and all snapshots should be considered as potentially satisfying the retention policy regardless of the name of the snapshot.  Only the creation property really matters unless the user configures zfsmgmt otherwise.  If the user wants to preserve a given snapshot it should be preserved using the zfs hold mechanism.  This allows zfs_mgmt to manage snapshots indepentantly of the mechanism used to create them.

