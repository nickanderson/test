# TEST #
antitoxic/diem@2b4514646177a95951202c4aea388cf472b53ca1

# Solutions - 01

1. Can you find a promise that is activated on any agent?
  * The promise with handle `main_methods_firewall_open_cf_serverd` is
    classed to `any::`.


2. Can you find a promise that is activated on agents that identify as a policy
hub?
  * The promise with handle `main_commands_report` is classed to `am_policy_hub::`.


3. Can you find a promise that is activated on agents that do not identify as a
policy hub?
  * The promise with handle `main_commands_echo_hi_wall` is classed to
    `!am_policy_hub.from_cfexecd::`. Promises after this class expression will be
    considered for activation on agents that do not have `am_policy_hub` defined and
    have `from_cfexecd` defined. `from_cfexecd` is an automatic class that is defined
    when the agent is executed from cf-execd.


4. Add a new promise to Shutdown/halt machines that execute the agent from
cf_execd and are not policy hubs
  * Add the following promise after `!am_policy_hub.from_cfexecd::`.

    ```
    "/sbin/shutdown"
      handle => "main_commands_shutdown",
      args => "-h now",
      comment => "Poweroff remote clients";
    ```

