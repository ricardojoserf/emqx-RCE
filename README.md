# EMQX Malicious Plugin

EMQX malicious plugin for EMQX >= 5.0.


## Prerequisites

 + A working build environment (eg `build_essential`) including `make`
 + Erlang OTP 25 or newer recommended
 + rebar3

## Usage

Create the folder and download the plugin code:

```shell
mkdir -p ~/.config/rebar3/templates/emqx-plugin-template
git clone https://github.com/ricardojoserf/emqx-RCE ~/.config/rebar3/templates/emqx-plugin-template
```

Optionally: Update the command you want to execute in [src/emqx_plugin_template.erl](src/emqx_plugin_template.erl) in line 47. 

```shell
rebar3 new emqx-plugin my_emqx_plugin
make -C my_emqx_plugin rel
```

This will create a tarball containing your custom plugin. You can use EMQX's Dashboard or it's command line tools to deploy it into your running EMQX cluster.

See [EMQX documentation](https://docs.emqx.com/en/enterprise/v5.0/extensions/plugins.html) for details on how to deploy custom plugins.
