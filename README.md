# EMQX Dashboard - RCE

This is a malicious plugin for [EMQX Dashboard](https://github.com/emqx/emqx-dashboard) which allows to execute commands remotely.

The code in this repository is mostly based on one of the latest releases of the [EMQX plugin template](https://github.com/emqx/emqx-plugin-template) repository.

If you would like to give this a try, you can launch a Docker image as explained in [EMQX docs](https://docs.emqx.com/en/emqx/latest/deploy/install-docker.html).

----------------------

## Plugin Compilation

1. Install all the necessary dependencies, Erlang and rebar3. In the latest Kali release (Kali 2024.4) you can use:

```shell
sudo apt update
sudo apt install -y build-essential autoconf libncurses5-dev libssl-dev \
    libwxgtk3.2-dev libgl1-mesa-dev libglu1-mesa-dev libpng-dev \
    libssh-dev unixodbc-dev cmake
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.13.1
echo '. "$HOME/.asdf/asdf.sh"' >> ~/.bashrc
echo '. "$HOME/.asdf/completions/asdf.bash"' >> ~/.bashrc
source ~/.bashrc
asdf --version
asdf plugin-add erlang https://github.com/asdf-vm/asdf-erlang.git
asdf install erlang 25.3
asdf global erlang 25.3
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
cp my_emqx_plugin/_build/default/emqx_plugrel/my_emqx_plugin-1.0.0.tar.gz . 
```

5. Install and run via the EMQX Dashboard under the "Plugin" section.

----------------------

## Disclosure

Following discussions with the EMQX security team in February and March 2025, they confirmed that this is not considered a vulnerability but rather a "feature" and have no objections to making this repository public.

However, starting from version 5.8.6 (released on 25/3/25), this feature will be mitigated by introducing "a CLI command to explicitly allow the package before installing a plugin via the HTTP API or Dashboard, improving security and preventing unauthorized installations" ([source](https://docs.emqx.com/en/emqx/latest/changes/changes-ce-v5.html#_5-8-6)).

Therefore, in earlier versions having access to the EMQX Dashboard you can achieve RCE, but in versions after 5.8.6 you will get this error:

![img](https://raw.githubusercontent.com/ricardojoserf/ricardojoserf.github.io/refs/heads/master/images/emqx/Screenshot_2.png)
