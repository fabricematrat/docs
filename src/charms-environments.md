[ ![Juju logo](//assets.ubuntu.com/sites/ubuntu/latest/u/img/logo.png) Juju
](https://juju.ubuntu.com/)

  - Jump to content
  - [Charms](https://juju.ubuntu.com/charms/)
  - [Features](https://juju.ubuntu.com/features/)
  - [Deploy](https://juju.ubuntu.com/deployment/)
  - [Resources](https://juju.ubuntu.com/resources/)
  - [Community](https://juju.ubuntu.com/community/)
  - [Install Juju](https://juju.ubuntu.com/download/)

Search: Search

## Juju documentation

LINKS

# Managing environments

Juju can be used to manage multiple clouds on different environments. The
environments themselves need only be defined in the `environments.yaml` file as
more fully described in the configuration section of the documentation. It is
entirely possible to have multiple environments with the same cloud provider
(providing they are of course separate environments on the cloud too) or across
all the different types of supported cloud providers.

## Identifying the current environment

The order of precedence for determining the environment a command will be
executed on is:

  1. The environment specified by the use of the `-e` switch.
  2. The environment set by the `JUJU_ENV` environment variable.
  3. The environment last specified with the `switch` command. 
  4. The environment specified as the default in `environments.yaml`.

To determine which environment a command will act on, you can issue the `switch`
command with no parameters:

    
    
    juju switch
    
    Current environment: "amazon" (from JUJU_ENV)
    

It is also possible to determine the current environment by checking the
`JUJU_ENV` variable, and if that is empty, the contents of the file `~/.juju
/current-environment`:

    
    
    echo $JUJU_ENV
    
    cat ~/.juju/current-environment 
    

## Specifying an environment

You can use the `-e` switch with a Juju command, followed by a valid environment
label, to specify that the command should be run against that environment. Using
the `-e` switch takes precedence over any other setting.

For example:

    
    
    juju bootstrap                 # bootstraps the default environment
    juju switch amazon             # switches the environment to the cloud defined by 'amazon'
    juju deploy mysql -e mycloud   # deploys mysql charm on the cloud defined by 'mycloud'
    

__Note: __ Unlike many switches used with juju, `-e` must come at the end of the
command in order to be parsed correctly.

## Switching environments

When managing several cloud environments, it can be bothersome to issue a long
list of commands and remember to prepend the `-e` switch to each one. For this
reason, you can switch the current environment using the `switch` command:

    
    
    juju switch hpcloud
    juju bootstrap  
    

... will bootstrap the environment defined by the 'hpcloud' label

This command will return with an error message if `JUJU_ENV`is set (as this
takes precedence).

__Note: __The environment selected with `switch` is persistent. Even if you log
out, switch your computer off, travel into space or sail around the world, when
you start using Juju again, it will still point at the last environment you
specified with `switch`.

## Default environment

The default environment is the environment which will be used if you have not
issued a `switch` command and do not specify an environment to use with the `-e`
switch or alter the `JUJU_ENV` environment variable. The default environment is
specified at the top of the `environments.yaml` file, before the environment
specifications themselves, like this:

    
    
    ...
    default: amazon
    
    environments:
      ## https://juju.ubuntu.com/docs/config-openstack.html
      openstack:
    ...
    

## Updating environments

Juju will attempt to maintain a high degree of legacy compatibility for the
environments.yaml definitions, so you should be able to update to stable
versions of the software without worring about reconfiguring your environments
each time. However, new releases do sometimes add support for new cloud
providers, add additional settings or change to adapt to configuration changes
for the providers themselves. In these cases it can be useful to generate a new
boilerplate `environments.yaml` so you can easily manually edit your own
configurations or cut and paste new environments into your existing
configuration.

To generate a new boilerplate `environments.yaml` file direct to the console you
can use:

    
    
    juju generate-config --show
    

Or:

    
    
    juju init --show
    

as the `init`command is an alias for `generate-config`.

  - ## [Juju](/)

    - [Charms](/charms)
    - [Features](/features)
    - [Deployment](/deployment)
  - ## [Resources](/resources)

    - [Overview](/resources/juju-overview/)
    - [Documentation](/docs/)
    - [The Juju web UI](/resources/the-juju-gui/)
    - [The charm store](/docs/authors-charm-store.html)
    - [Tutorial](/docs/getting-started.html#test)
    - [Videos](/resources/videos/)
    - [Easy tasks for new developers](/resources/easy-tasks-for-new-developers/)
  - ## [Community](/community)

    - [Juju Blog](/community/blog/)
    - [Events](/events/)
    - [Weekly charm meeting](/community/weekly-charm-meeting/)
    - [Charmers](/community/charmers/)
    - [Write a charm](/docs/authors-charm-writing.html)
    - [Help with documentation](/docs/contributing.html)
    - [File a bug](https://bugs.launchpad.net/juju-core/+filebug)
    - [Juju Labs](/labs/)
  - ## [Try Juju](https://jujucharms.com/sidebar/)

    - [Charm store](https://jujucharms.com/)
    - [Download Juju](/download/)

(C) 2013 Canonical Ltd. Ubuntu and Canonical are registered trademarks of
[Canonical Ltd](http://canonical.com).
