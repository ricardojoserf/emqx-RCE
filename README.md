# EMQX Dashboard - RCE

This is a malicious plugin for [EMQX Dashboard](https://github.com/emqx/emqx-dashboard) which allows to execute commands remotely.

The code in this repository is mostly based on one of the latest releases of the [EMQX plugin template](https://github.com/emqx/emqx-plugin-template) repository.


----------------------

## Prerequisites

To build and use this plugin, ensure you have:

 + A working build environment (eg `build_essential`) including `make`
 + Erlang OTP 25 or newer recommended
 + rebar3


----------------------

## Compilation

1. Create the necessary directory and clone the plugin repository:

```shell
mkdir -p ~/.config/rebar3/templates/emqx-plugin-template
git clone https://github.com/ricardojoserf/emqx-RCE ~/.config/rebar3/templates/emqx-plugin-template
```

2. (Optional) Modify the command to be executed by updating line 47 in [src/emqx_plugin_template.erl](src/emqx_plugin_template.erl). By default, it creates a text file at /tmp/poc.txt.

3. Generate the plugin and build it:

```shell
rebar3 new emqx-plugin my_emqx_plugin
make -C my_emqx_plugin rel
```

This process will generate a tarball containing the plugin. Install it via the EMQX Dashboard under the "Plugin" section.


----------------------

## Disclosure

Following discussions with the EMQX security team, they do not consider this a vulnerability and have no objections to this repository being public.
