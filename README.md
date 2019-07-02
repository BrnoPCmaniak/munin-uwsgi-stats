# munin-uwsgi-stats

Detailed uWSGI stats plugin for munin

## Prerequisites

- **uWSGI**
- **munin**
- **Python**

## Install:

- Download a plugin file appropriate to your situation ( [uwsgi_multi_](https://github.com/PF4Public/munin-uwsgi-stats/raw/master/uwsgi_multi_) or [uwsgi_](https://github.com/PF4Public/munin-uwsgi-stats/raw/master/uwsgi_) ). `uwsgi_` combines all the workers by summing/averaging their statistics, whereas `uwsgi_multi_` provides statistics for every worker separately.
- Make it executable via `chmod +x`

## Config & test:

1. Activate and configure stats server in your uWSGI installation (see [uWSGI Documentation](http://uwsgi-docs.readthedocs.io/en/latest/StatsServer.html) for more information). If you plan on obtaining memory statistics, you need to enable `memory-report = true` uWSGI option. If you use `stats-http` option you have to specify `http://` in env.addr.
2. Restart uWSGI. Verify that stats are activated and that there is a JSON output at your configured `host:port`, using `wget -O - 127.0.0.1:49000` or `nc 127.0.0.1 49000`.
3. Edit `/etc/munin/plugin-conf.d/munin-node` to reflect your uWSGI stats setting, e.g.:

  [uwsgi_*]<br>
  env.addr 127.0.0.1:49000

4. Use `munin-node-configure --shell` to aid creating all the necessary plugin symlinks

5. Verify that everything is fine with `munin-run uwsgi_avg_rt` for example

## Graph multiple UWSGI on single host

You can easily graph multiple application on single host by simply naming the files as:

`uwsgi-<APP_NAME>_multi_`

This allows you to set in munin-node different addresses for each app

## License:

This project is licensed under the terms of the BSD license.

## Related work:

- [xrmx/uwsgitop project](https://github.com/xrmx/uwsgitop)
- [jarus/munin-uwsgi project](https://github.com/jarus/munin-uwsgi) - this one only tracks memory & processes
- [lambdaq/munin-uwsgi-stats project](https://github.com/lambdaq/munin-uwsgi-stats) - this one uses `psutils` for memory statistics therefore needs to be run as `root` or your uwsgi-user
- [shadowfax-chc/munin-uwsgi-stats project](https://github.com/shadowfax-chc/munin-uwsgi-stats) - this project is the origin for my fork

## Acknowledgements

### Original authors

- lambdaq, <https://github.com/lambdaq>
- Timothy Messier, <https://github.com/shadowfax-chc>

### List of contributors

For a complete list of contributors, refer to [Github project contributors page](https://github.com/PF4Public/munin-uwsgi-stats/graphs/contributors)
