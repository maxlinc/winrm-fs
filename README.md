# File system operations over Windows Remote Management (WinRM) for Ruby
[![Build Status](https://travis-ci.org/WinRb/winrm-fs.svg?branch=master)](https://travis-ci.org/WinRb/winrm-fs)
[![Gem Version](https://badge.fury.io/rb/winrm-fs.svg)](http://badge.fury.io/rb/winrm-fs)

## Uploading files
Files may be copied from the local machine to the winrm endpoint. Individual
files or directories may be specified:
```ruby
require 'winrm-fs'

service = WinRM::WinRMWebService.new(...
file_manager = WinRM::FS::FileManager.new(service)
file_manager.upload('c:/dev/my_dir', '$env:AppData')
```
Or an array of several files and/or directories can be included:
```ruby
file_manager.upload(['c:/dev/file1.txt','c:/dev/dir1'], '$env:AppData')
```

### Handling progress events
If you want to implemnt your own custom progress handling, you can pass a code
block and use the proggress data that `upload` yields to this block:
```ruby
file_manager.upload('c:/dev/my_dir', '$env:AppData') do |bytes_copied, total_bytes, local_path, remote_path|
  puts "#{bytes_copied}bytes of #{total_bytes}bytes copied"
end
```

## Contributing

1. Fork it.
2. Create a branch (git checkout -b my_feature_branch)
3. Run the unit and integration tests (bundle exec rake integration)
4. Commit your changes (git commit -am "Added a sweet feature")
5. Push to the branch (git push origin my_feature_branch)
6. Create a pull requst from your branch into master (Please be sure to provide enough detail for us to cipher what this change is doing)

### Running the tests

We use Bundler to manage dependencies during development.

```
$ bundle install
```

Once you have the dependencies, you can run the unit tests with `rake`:

```
$ bundle exec rake spec
```

To run the integration tests you will need a Windows box with the WinRM service properly configured. Its easiest to use the Vagrant Windows box in the Vagrantilfe of this repo.

1. Create a Windows VM with WinRM configured (see above).
2. Copy the config-example.yml to config.yml - edit this file with your WinRM connection details.
3. Run `bundle exec rake integration`

## WinRM-fs Authors
* Shawn Neal (https://github.com/sneal)
* Matt Wrock (https://github.com/mwrock)

[Contributors](https://github.com/WinRb/winrm-fs/graphs/contributors)
