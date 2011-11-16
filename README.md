smartcloud
===

Provides support for interacting with IBM SmartCloud API and CLI tools

installation
===

from rubygems.org:

    gem install cft_smartcloud

locally:

    rake build
    gem install pkg/[name of generated gem]

setup
===

Please set up SMARTCLOUD_USERNAME and SMARTCLOUD_PASSWORD in your .bash_profile

    export SMARTCLOUD_USERNAME=[your username]
    export SMARTCLOUD_PASSWORD=[your password]

You can now also supply the username and password on the command line using -u and -p
Use `smartcloud help` to get a list of all optoins.

screencast
===

http://www.youtube.com/cohesiveft#p/u/0/-WdSHP2iwDM (somewhat outdated)

using the console
== 

    script/console
    >> @smartcloud.display_instances
    >> @smartcloud.display_volumes(:Location => 101)
    >> @smartcloud.display_instances(:Location => 82, :Name => "namematch")
    >> @smartcloud.poll_for_volume_state(12345, :unmounted)

  The console predefines the @smartcloud instance variable that is set up
  from the environment variables SMARTCLOUD_USERNAME and SMARTCLOUD_PASSWORD
  automatically (it's created at the bottom of smartcloud.rb)

using the commandline helper
== 

    smartcloud [method of smartcloud.rb]

to see a list of methods:

    smartcloud help

examples:

      smartcloud display_volumes
      smartcloud display_instances
      smartcloud display_instance 12345
      smartcloud delete_instances 12345 12346 12347
      smartcloud "describe_instance('12345')"
      smartcloud "display_instances(:Location => 82, :Name => 'match_this')"

      smartcloud delete_unused_keys # this one will prompt for every key

The 'display_*' methods are intended to generate pretty human readable displays, while the describe methods
will return pretty-formatted hashes, or singular values.

      smartcloud display_volumes

get a list of all available methods
===

console:

      >> @smartcloud.help

commandline

      > smartcloud help

These won't tell you the arguments, you have to look at smartcloud.rb for the args.

RestClient vs CurlHttpClient
===
Sometimes RestClient and friends have trouble communicating with certain API's such as 
IBM SmartCloud, returning 500 errors. We found in some cases the only thing that truly
works is pure curl (not even libcurl ruby wrappers). Therefore there is a provided 
simple CurlHttpClient library which emulates the RestClient interface, and wraps 
command line calls to curl.

The choice of client is determined inside of config.yml

Versioning
== 

This project uses the jeweler gem for packaging. See the tasks:

    rake version:bump:...
    rake build

Copyright
== 

Copyright (c) 2011 CohesiveFT. See LICENSE for details.
