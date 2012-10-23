# TEST #
antitoxic/diem@2b4514646177a95951202c4aea388cf472b53ca1

# Investigate Seed Policy

A bare git repository (masterfiles.git) was created as part of the project
initilization.  The policy server aka policy hub or just hub is configured to
keep its `/var/cfengine/masterfiles` in sync with this repository. This
repository is how you will interface with your policy. Clone it so that you have
a working copy.

    $ git clone masterfiles.git
    Cloning into 'masterfiles'...
    done.
    $ cd masterfiles
    $ ls
    controls  failsafe.cf  main.cf      reporter_text.cf
    def.cf    libraries    promises.cf  sketches


Take a look the current policy. Remember promises.cf is the first file read by
the agent, so thats a good place to start.

## body common control

body common control is a required part of any CFEngine
policy. CFEngine executes agent promise bundles in the strict order defined by
the bundlesequence (possibly overridden by the -b or --bundlesequence command
line option). This is a great place to figure out the policy that may be
activated by a given agent based on the classes defined.

Get used to searching the policy. This is a useful search to locate a bundle of
any type by name. `find . -type f | xargs grep "bundle\s.*\sBUNDLENAME"`

    $ find . -type f | xargs grep "bundle\s.*\smain"
    ./sketches/VCS/vcs_mirror/README.md:    bundle agent main {
    ./main.cf:bundle agent main

Two matches found, one is in a README, the other is in main.cf. That seems like
a good place to start looking.

Read the policy in main.cf.

## Exercises

#. Can you find a promise that is activated on any agent?

#. Can you find a promise that is activated on agents that identify as a policy
hub?

#. Can you find a promise that is activated on agents that do not identify as a
policy hub? 

#. Add a new promise to Shutdown/halt machines that execute the agent from
cf_execd and are not policy hubs

