# EMQX Dashboard - RCE

This is a malicious plugin for [EMQX Dashboard](https://github.com/emqx/emqx-dashboard) which allows to execute commands remotely.

The code in this repository is mostly based on one of the latest releases of the [EMQX plugin template](https://github.com/emqx/emqx-plugin-template) repository.


----------------------

## Plugin Compilation

1. Install make, cmake, Erlang and rebar3.

```shell
sudo apt install -y make cmake build-essential libssl-dev libncurses5-dev
sudo apt install -y erlang
wget https://s3.amazonaws.com/rebar3/rebar3
chmod +x rebar3
sudo mv rebar3 /usr/local/bin/
```

2. Create the necessary directory and clone the plugin repository:

```shell
mkdir -p ~/.config/rebar3/templates/emqx-plugin-template
git clone https://github.com/ricardojoserf/emqx-RCE ~/.config/rebar3/templates/emqx-plugin-template
```

3. (Optional) Modify the command to be executed by updating line 47 in "src/emqx_plugin_template.erl":

![img](https://raw.githubusercontent.com/ricardojoserf/ricardojoserf.github.io/refs/heads/master/images/emqx/Screenshot_1.png)

4. Generate the plugin as a tar.gz file:

```shell
rebar3 new emqx-plugin my_emqx_plugin
make -C my_emqx_plugin rel
```

5. Install and run via the EMQX Dashboard under the "Plugin" section.

----------------------

## Disclosure

Following discussions with the EMQX security team, they do not consider this a vulnerability but a "feature" and have no objections to this repository being public.

However, versions 5.8.6 and higher will mitigate this feature by not using default credentials and disabling the plugin installation from the dashboard (it will only be available through the CLI).
