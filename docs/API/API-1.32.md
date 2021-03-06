This is the list of commands and modifiers available for
dbdeployer 1.32.0 as of 09-Jun-2019 15:54 UTC

# main
    $ dbdeployer -h 
    dbdeployer makes MySQL server installation an easy task.
    Runs single, multiple, and replicated sandboxes.
    
    Usage:
      dbdeployer [command]
    
    Available Commands:
      admin           sandbox management tasks
      cookbook        Shows dbdeployer samples
      defaults        tasks related to dbdeployer defaults
      delete          delete an installed sandbox
      delete-binaries delete an expanded tarball
      deploy          deploy sandboxes
      downloads       Manages remote tarballs
      export          Exports the command structure in JSON format
      global          Runs a given command in every sandbox
      help            Help about any command
      info            Shows information about dbdeployer environment samples
      sandboxes       List installed sandboxes
      unpack          unpack a tarball into the binary directory
      usage           Shows usage of installed sandboxes
      versions        List available versions
    
    Flags:
          --config string           configuration file (default "$HOME/.dbdeployer/config.json")
      -h, --help                    help for dbdeployer
          --sandbox-binary string   Binary repository (default "$HOME/opt/mysql")
          --sandbox-home string     Sandbox deployment directory (default "$HOME/sandboxes")
          --shell-path string       Which shell to use for generated scripts (default "/bin/bash")
          --version                 version for dbdeployer
    
    Use "dbdeployer [command] --help" for more information about a command.
    

    $ dbdeployer-docs tree 
    - admin               
        - capabilities        
        - lock                
        - unlock              
        - upgrade             
    - cookbook            
        - create              
        - list                
        - show                
    - defaults            
        - export              
        - load                
        - reset               
        - show                
        - store               
        - templates           
            - describe            
            - export              
            - import              
            - list                
            - reset               
            - show                
        - update              
    - delete              
    - delete-binaries     
    - deploy              
        - multiple            
        - replication         
        - single              
    - downloads           
        - export              
        - get                 
        - get-by-version      
        - import              
        - list                
        - reset               
        - show                
    - export              
    - global              
        - restart             
        - start               
        - status              
        - stop                
        - test                
        - test-replication    
        - use                 
    - info                
        - defaults            
        - version             
    - remote              
        - download            
        - list                
    - sandboxes           
    - unpack              
    - usage               
    - versions            
    

## admin
    $ dbdeployer admin -h
    Runs commands related to the administration of sandboxes.
    
    Usage:
      dbdeployer admin [command]
    
    Aliases:
      admin, manage
    
    Available Commands:
      capabilities Shows capabilities of a given flavor [and optionally version]
      lock         Locks a sandbox, preventing deletion
      unlock       Unlocks a sandbox
      upgrade      Upgrades a sandbox to a newer version
    
    Flags:
      -h, --help   help for admin
    
    
    $ dbdeployer admin capabilities -h
    Shows the capabilities of all flavors. 
    If a flavor is specified, only the capabilities of that flavor are shown.
    If also a version is specified, we show what that version supports
    
    Usage:
      dbdeployer admin capabilities [flavor [version]] [flags]
    
    Examples:
    dbdeployer admin capabilities
    dbdeployer admin capabilities mysql
    dbdeployer admin capabilities mysql 5.7.11
    dbdeployer admin capabilities mysql 5.7.13
    
    
    Flags:
      -h, --help   help for capabilities
    
    
    $ dbdeployer admin lock -h
    Prevents deletion for a given sandbox.
    Note that the deletion being prevented is only the one occurring through dbdeployer. 
    Users can still delete locked sandboxes manually.
    
    Usage:
      dbdeployer admin lock sandbox_name [flags]
    
    Aliases:
      lock, preserve
    
    Flags:
      -h, --help   help for lock
    
    
    $ dbdeployer admin unlock -h
    Removes lock, allowing deletion of a given sandbox
    
    Usage:
      dbdeployer admin unlock sandbox_name [flags]
    
    Aliases:
      unlock, unpreserve
    
    Flags:
      -h, --help   help for unlock
    
    
    $ dbdeployer admin upgrade -h
    Upgrades a sandbox to a newer version.
    The sandbox with the new version must exist already.
    The data directory of the old sandbox will be moved to the new one.
    
    Usage:
      dbdeployer admin upgrade sandbox_name newer_sandbox [flags]
    
    Examples:
    dbdeployer admin upgrade msb_8_0_11 msb_8_0_12
    
    Flags:
          --dry-run   Shows upgrade operations, but don't execute them
      -h, --help      help for upgrade
          --verbose   Shows upgrade operations
    
    

## cookbook
    $ dbdeployer cookbook -h
    Shows practical examples of dbdeployer usages, by creating usage scripts.
    
    Usage:
      dbdeployer cookbook [command]
    
    Aliases:
      cookbook, recipes, samples
    
    Available Commands:
      create      creates a script for a given recipe
      list        Shows available dbdeployer samples
      show        Shows the contents of a given recipe
    
    Flags:
          --flavor string   For which flavor this recipe is
      -h, --help            help for cookbook
    
    
    $ dbdeployer cookbook create -h
    creates a script for a given recipe
    
    Usage:
      dbdeployer cookbook create recipe_name or ALL [flags]
    
    Aliases:
      create, make
    
    Flags:
      -h, --help   help for create
    
    
    $ dbdeployer cookbook list -h
    Shows list of available cookbook recipes
    
    Usage:
      dbdeployer cookbook list [flags]
    
    Flags:
      -h, --help             help for list
          --sort-by string   Sort order for the list (name, flavor, script) (default "name")
    
    
    $ dbdeployer cookbook show -h
    Shows the contents of a given recipe, without actually running it
    
    Usage:
      dbdeployer cookbook show recipe_name [flags]
    
    Flags:
      -h, --help   help for show
          --raw    Shows the recipe without variable substitution
    
    

## defaults
    $ dbdeployer defaults -h
    Runs commands related to the administration of dbdeployer,
    such as showing the defaults and saving new ones.
    
    Usage:
      dbdeployer defaults [command]
    
    Aliases:
      defaults, config
    
    Available Commands:
      export      Export current defaults to a given file
      load        Load defaults from file
      reset       Remove current defaults file
      show        shows defaults
      store       Store current defaults
      templates   Templates management
      update      Change defaults value
    
    Flags:
      -h, --help   help for defaults
    
    
    $ dbdeployer defaults export -h
    Saves current defaults to a user-defined file
    
    Usage:
      dbdeployer defaults export filename [flags]
    
    Flags:
      -h, --help   help for export
    
    
    $ dbdeployer defaults load -h
    Reads defaults from file and saves them to dbdeployer configuration file ($HOME/.dbdeployer/config.json)
    
    Usage:
      dbdeployer defaults load file_name [flags]
    
    Aliases:
      load, import
    
    Flags:
      -h, --help   help for load
    
    
    $ dbdeployer defaults reset -h
    Removes current dbdeployer configuration file ($HOME/.dbdeployer/config.json)
    Afterwards, dbdeployer will use the internally stored defaults.
    
    Usage:
      dbdeployer defaults reset [flags]
    
    Aliases:
      reset, remove
    
    Flags:
      -h, --help   help for reset
    
    
    $ dbdeployer defaults show -h
    Shows currently defined defaults
    
    Usage:
      dbdeployer defaults show [flags]
    
    Aliases:
      show, list
    
    Flags:
      -h, --help   help for show
    
    
    $ dbdeployer defaults store -h
    Saves current defaults to dbdeployer configuration file ($HOME/.dbdeployer/config.json)
    
    Usage:
      dbdeployer defaults store [flags]
    
    Flags:
      -h, --help   help for store
    
    

## defaults templates
    $ dbdeployer defaults templates -h
    The commands in this section show the templates used
    to create and manipulate sandboxes.
    
    Usage:
      dbdeployer defaults templates [command]
    
    Aliases:
      templates, template, tmpl, templ
    
    Available Commands:
      describe    Describe a given template
      export      Exports templates to a directory
      import      imports templates from a directory
      list        list available templates
      reset       Removes all template files
      show        Show a given template
    
    Flags:
      -h, --help   help for templates
    
    
    $ dbdeployer defaults templates describe -h
    Describe a given template
    
    Usage:
      dbdeployer defaults templates describe template_name [flags]
    
    Aliases:
      describe, descr, structure, struct
    
    Flags:
      -h, --help            help for describe
          --with-contents   Shows complete structure and contents
    
    
    $ dbdeployer defaults templates export -h
    Exports a group of templates (or "ALL") to a given directory
    
    Usage:
      dbdeployer defaults templates export group_name directory_name [template_name] [flags]
    
    Flags:
      -h, --help   help for export
    
    
    $ dbdeployer defaults templates import -h
    Imports a group of templates (or "ALL") from a given directory
    
    Usage:
      dbdeployer defaults templates import group_name directory_name [template_name] [flags]
    
    Flags:
      -h, --help   help for import
    
    
    $ dbdeployer defaults templates list -h
    list available templates
    
    Usage:
      dbdeployer defaults templates list [group] [flags]
    
    Flags:
      -h, --help     help for list
      -s, --simple   Shows only the template names, without description
    
    
    $ dbdeployer defaults templates reset -h
    Removes all template files that were imported and starts using internal values.
    
    Usage:
      dbdeployer defaults templates reset [flags]
    
    Aliases:
      reset, remove
    
    Flags:
      -h, --help   help for reset
    
    
    $ dbdeployer defaults templates show -h
    Show a given template
    
    Usage:
      dbdeployer defaults templates show template_name [flags]
    
    Flags:
      -h, --help   help for show
    
    
    $ dbdeployer defaults update -h
    Updates one field of the defaults. Stores the result in the dbdeployer configuration file.
    Use "dbdeployer defaults show" to see which values are available
    
    Usage:
      dbdeployer defaults update label value [flags]
    
    Examples:
    
    	$ dbdeployer defaults update master-slave-base-port 17500		
    
    
    Flags:
      -h, --help   help for update
    
    

## delete
    $ dbdeployer delete -h
    Stops the sandbox (and its depending sandboxes, if any), and removes it.
    Warning: this command is irreversible!
    
    Usage:
      dbdeployer delete sandbox_name (or "ALL") [flags]
    
    Aliases:
      delete, remove, destroy
    
    Examples:
    
    	$ dbdeployer delete msb_8_0_4
    	$ dbdeployer delete rsandbox_5_7_21
    
    Flags:
          --concurrent     Runs multiple deletion tasks concurrently.
          --confirm        Requires confirmation.
      -h, --help           help for delete
          --skip-confirm   Skips confirmation with multiple deletions.
    
    

## delete-binaries
    $ dbdeployer delete-binaries -h
    Removes the given directory and all its subdirectories.
    It will fail if the directory is still used by any sandbox.
    Warning: this command is irreversible!
    
    Usage:
      dbdeployer delete-binaries binaries_dir_name [flags]
    
    Examples:
    
    	$ dbdeployer delete-binaries 8.0.4
    	$ dbdeployer delete ps5.7.25
    
    Flags:
      -h, --help           help for delete-binaries
          --skip-confirm   Skips confirmation.
    
    

## deploy
    $ dbdeployer deploy -h
    Deploys single, multiple, or replicated sandboxes
    
    Usage:
      dbdeployer deploy [command]
    
    Available Commands:
      multiple    create multiple sandbox
      replication create replication sandbox
      single      deploys a single sandbox
    
    Flags:
          --base-port int                 Overrides default base-port (for multiple sandboxes)
          --binary-version string         Specifies the version when the basedir directory name does not contain it (i.e. it is not x.x.xx)
          --bind-address string           defines the database bind-address  (default "127.0.0.1")
          --client-from string            Where to get the client binaries from
          --concurrent                    Runs multiple sandbox deployments concurrently
          --custom-mysqld string          Uses an alternative mysqld (must be in the same directory as regular mysqld)
      -p, --db-password string            database password (default "msandbox")
      -u, --db-user string                database user (default "msandbox")
          --defaults strings              Change defaults on-the-fly (--defaults=label:value)
          --disable-mysqlx                Disable MySQLX plugin (8.0.11+)
          --enable-admin-address          Enables admin address (8.0.14+)
          --enable-general-log            Enables general log for the sandbox (MySQL 5.1+)
          --enable-mysqlx                 Enables MySQLX plugin (5.7.12+)
          --expose-dd-tables              In MySQL 8.0+ shows data dictionary tables
          --flavor string                 Defines the tarball flavor (MySQL, NDB, Percona Server, etc)
          --flavor-in-prompt              Add flavor values to prompt
          --force                         If a destination sandbox already exists, it will be overwritten
          --gtid                          enables GTID
      -h, --help                          help for deploy
          --history-dir string            Where to store mysql client history (default: in sandbox directory)
          --init-general-log              uses general log during initialization (MySQL 5.1+)
      -i, --init-options strings          mysqld options to run during initialization
          --keep-server-uuid              Does not change the server UUID
          --log-directory string          Where to store dbdeployer logs (default "$HOME/sandboxes/logs")
          --log-sb-operations             Logs sandbox operations to a file
          --my-cnf-file string            Alternative source file for my.sandbox.cnf
      -c, --my-cnf-options strings        mysqld options to add to my.sandbox.cnf
          --native-auth-plugin            in 8.0.4+, uses the native password auth plugin
          --port int                      Overrides default port
          --port-as-server-id             Use the port number as server ID
          --post-grants-sql strings       SQL queries to run after loading grants
          --post-grants-sql-file string   SQL file to run after loading grants
          --pre-grants-sql strings        SQL queries to run before loading grants
          --pre-grants-sql-file string    SQL file to run before loading grants
          --remote-access string          defines the database access  (default "127.%")
          --repl-crash-safe               enables Replication crash safe
          --rpl-password string           replication password (default "rsandbox")
          --rpl-user string               replication user (default "rsandbox")
          --sandbox-directory string      Changes the default sandbox directory
          --skip-load-grants              Does not load the grants
          --skip-report-host              Does not include report host in my.sandbox.cnf
          --skip-report-port              Does not include report port in my.sandbox.cnf
          --skip-start                    Does not start the database server
          --socket-in-datadir             Create socket in datadir instead of $TMPDIR
          --use-template strings          [template_name:file_name] Replace existing template with one from file
    
    
    $ dbdeployer deploy multiple -h
    Creates several sandboxes of the same version,
    without any replication relationship.
    For this command to work, there must be a directory $HOME/opt/mysql/5.7.21, containing
    the binary files from mysql-5.7.21-$YOUR_OS-x86_64.tar.gz
    Use the "unpack" command to get the tarball into the right directory.
    
    Usage:
      dbdeployer deploy multiple MySQL-Version [flags]
    
    Examples:
    
    	$ dbdeployer deploy multiple 5.7.21
    	
    
    Flags:
      -h, --help        help for multiple
      -n, --nodes int   How many nodes will be installed (default 3)
    
    
    $ dbdeployer deploy replication -h
    The replication command allows you to deploy several nodes in replication.
    Allowed topologies are "master-slave" for all versions, and  "group", "all-masters", "fan-in"
    for  5.7.17+.
    Topologies "pcx" and "ndb" are available for binaries of type Percona Xtradb Cluster and MySQL Cluster.
    For this command to work, there must be a directory $HOME/opt/mysql/5.7.21, containing
    the binary files from mysql-5.7.21-$YOUR_OS-x86_64.tar.gz
    Use the "unpack" command to get the tarball into the right directory.
    
    Usage:
      dbdeployer deploy replication MySQL-Version [flags]
    
    Examples:
    
    		$ dbdeployer deploy replication 5.7    # deploys highest revision for 5.7
    		$ dbdeployer deploy replication 5.7.21 # deploys a specific revision
    		$ dbdeployer deploy replication /path/to/5.7.21 # deploys a specific revision in a given path
    		# (implies topology = master-slave)
    
    		$ dbdeployer deploy --topology=master-slave replication 5.7
    		# (explicitly setting topology)
    
    		$ dbdeployer deploy --topology=group replication 5.7
    		$ dbdeployer deploy --topology=group replication 8.0 --single-primary
    		$ dbdeployer deploy --topology=all-masters replication 5.7
    		$ dbdeployer deploy --topology=fan-in replication 5.7
    		$ dbdeployer deploy --topology=pxc replication pxc5.7.25
    		$ dbdeployer deploy --topology=ndb replication ndb8.0.14
    	
    
    Flags:
      -h, --help                     help for replication
          --master-ip string         Which IP the slaves will connect to (default "127.0.0.1")
          --master-list string       Which nodes are masters in a multi-source deployment (default "1,2")
          --ndb-nodes int            How many NDB nodes will be installed (default 3)
      -n, --nodes int                How many nodes will be installed (default 3)
          --read-only-slaves         Set read-only for slaves
          --repl-history-dir         uses the replication directory to store mysql client history
          --semi-sync                Use semi-synchronous plugin
          --single-primary           Using single primary for group replication
          --slave-list string        Which nodes are slaves in a multi-source deployment (default "3")
          --super-read-only-slaves   Set super-read-only for slaves
      -t, --topology string          Which topology will be installed (default "master-slave")
    
    
    $ dbdeployer deploy single -h
    single installs a sandbox and creates useful scripts for its use.
    MySQL-Version is in the format x.x.xx, and it refers to a directory named after the version
    containing an unpacked tarball. The place where these directories are found is defined by 
    --sandbox-binary (default: $HOME/opt/mysql.)
    For example:
    	dbdeployer deploy single 5.7     # deploys the latest release of 5.7.x
    	dbdeployer deploy single 5.7.21  # deploys a specific release
    	dbdeployer deploy single /path/to/5.7.21  # deploys a specific release in a given path
    
    For this command to work, there must be a directory $HOME/opt/mysql/5.7.21, containing
    the binary files from mysql-5.7.21-$YOUR_OS-x86_64.tar.gz
    Use the "unpack" command to get the tarball into the right directory.
    
    Usage:
      dbdeployer deploy single MySQL-Version [flags]
    
    Flags:
      -h, --help            help for single
          --master          Make the server replication ready
          --prompt string   Default prompt for the single client (default "mysql")
    
    

## downloads
    $ dbdeployer downloads -h
    Manages remote tarballs
    
    Usage:
      dbdeployer downloads [command]
    
    Available Commands:
      export         Exports the list of tarballs to a file
      get            Downloads a remote tarball
      get-by-version Downloads a remote tarball
      import         Imports the list of tarballs from a file
      list           list remote tarballs
      reset          Reset the custom list of tarballs and resume the defaults
      show           Downloads a remote tarball
    
    Flags:
      -h, --help   help for downloads
    
    
    $ dbdeployer downloads export -h
    Exports the list of tarballs to a file
    
    Usage:
      dbdeployer downloads export file-name [options] [flags]
    
    Flags:
          --add-empty-item   Add an empty item to the tarballs list
      -h, --help             help for export
    
    
    $ dbdeployer downloads get -h
    Downloads a remote tarball
    
    Usage:
      dbdeployer downloads get tarball_name [options] [flags]
    
    Flags:
          --dry-run             Show what would be downloaded, but don't run it
      -h, --help                help for get
          --progress-step int   Progress interval (default 10485760)
          --quiet               Do not show download progress
    
    
    $ dbdeployer downloads get-by-version -h
    
    Download a tarball identified by a combination of
    version, flavor, operating system, and optionally its minimal state.
    If you don't specify the Operating system, the current one will be assumed.
    If the flavor is not specified, 'mysql' is assumed.
    Use the option '--dry-run' to see what dbdeployer would download.
    
    Usage:
      dbdeployer downloads get-by-version version [options] [flags]
    
    Examples:
    
    $ dbdeployer downloads get-by-version 5.7 --newest --dry-run
    $ dbdeployer downloads get-by-version 5.7 --newest --minimal --dry-run --OS=linux
    $ dbdeployer downloads get-by-version 5.7 --newest
    $ dbdeployer downloads get-by-version 8.0 --flavor=ndb
    $ dbdeployer downloads get-by-version 5.7.26 --minimal
    $ dbdeployer downloads get-by-version 5.7 --minimal
    
    
    Flags:
          --OS string           Choose only the given OS
          --dry-run             Show what would be downloaded, but don't run it
          --flavor string       Choose only the given flavor
      -h, --help                help for get-by-version
          --minimal             Choose only minimal tarballs
          --newest              Choose only the newest tarballs not yet downloaded
          --progress-step int   Progress interval (default 10485760)
          --quiet               Do not show download progress
    
    
    $ dbdeployer downloads import -h
    Imports the list of tarballs from a file
    
    Usage:
      dbdeployer downloads import file-name [options] [flags]
    
    Flags:
      -h, --help   help for import
    
    
    $ dbdeployer downloads list -h
    list remote tarballs
    
    Usage:
      dbdeployer downloads list [options] [flags]
    
    Aliases:
      list, index
    
    Flags:
          --OS string       Which OS will be listed
          --flavor string   Which flavor will be listed
      -h, --help            help for list
          --show-url        Show the URL
    
    
    $ dbdeployer downloads reset -h
    Reset the custom list of tarballs and resume the defaults
    
    Usage:
      dbdeployer downloads reset [flags]
    
    Flags:
      -h, --help   help for reset
    
    
    $ dbdeployer downloads show -h
    Downloads a remote tarball
    
    Usage:
      dbdeployer downloads show tarball_name [flags]
    
    Aliases:
      show, display
    
    Flags:
      -h, --help   help for show
    
    

## export
    $ dbdeployer export -h
    Exports the command line structure, with examples and flags, to a JSON structure.
    If a command is given, only the structure of that command and below will be exported.
    Given the length of the output, it is recommended to pipe it to a file or to another command.
    
    Usage:
      dbdeployer export [command [sub-command]] [ > filename ] [ | command ]  [flags]
    
    Aliases:
      export, dump
    
    Flags:
          --force-output-to-terminal   display output to terminal regardless of pipes being used
      -h, --help                       help for export
    
    

## global
    $ dbdeployer global -h
    This command can propagate the given action through all sandboxes.
    
    Usage:
      dbdeployer global [command]
    
    Examples:
    
    	$ dbdeployer global use "select version()"
    	$ dbdeployer global status
    	$ dbdeployer global stop
    	
    
    Available Commands:
      restart          Restarts all sandboxes
      start            Starts all sandboxes
      status           Shows the status in all sandboxes
      stop             Stops all sandboxes
      test             Tests all sandboxes
      test-replication Tests replication in all sandboxes
      use              Runs a query in all sandboxes
    
    Flags:
      -h, --help   help for global
    
    
    $ dbdeployer global restart -h
    Restarts all sandboxes
    
    Usage:
      dbdeployer global restart [options] [flags]
    
    Flags:
      -h, --help   help for restart
    
    
    $ dbdeployer global start -h
    Starts all sandboxes
    
    Usage:
      dbdeployer global start [options] [flags]
    
    Flags:
      -h, --help   help for start
    
    
    $ dbdeployer global status -h
    Shows the status in all sandboxes
    
    Usage:
      dbdeployer global status [flags]
    
    Flags:
      -h, --help   help for status
    
    
    $ dbdeployer global stop -h
    Stops all sandboxes
    
    Usage:
      dbdeployer global stop [flags]
    
    Flags:
      -h, --help   help for stop
    
    
    $ dbdeployer global test -h
    Tests all sandboxes
    
    Usage:
      dbdeployer global test [flags]
    
    Aliases:
      test, test_sb, test-sb
    
    Flags:
      -h, --help   help for test
    
    
    $ dbdeployer global test-replication -h
    Tests replication in all sandboxes
    
    Usage:
      dbdeployer global test-replication [flags]
    
    Aliases:
      test-replication, test_replication
    
    Flags:
      -h, --help   help for test-replication
    
    
    $ dbdeployer global use -h
    Runs a query in all sandboxes.
    It does not check if the query is compatible with every version deployed.
    For example, a query using @@port won't run in MySQL 5.0.x
    
    Usage:
      dbdeployer global use {query} [flags]
    
    Examples:
    
    	$ dbdeployer global use "select @@server_id, @@port"
    
    Flags:
      -h, --help   help for use
    
    

## info
    $ dbdeployer info -h
    Shows current information about defaults and environment.
    
    Usage:
      dbdeployer info [command]
    
    Available Commands:
      defaults    displays a defaults value
      version     displays the latest version available
    
    Flags:
          --flavor string   For which flavor this info is
      -h, --help            help for info
    
    
    $ dbdeployer info defaults -h
    Displays one field of the defaults.
    
    Usage:
      dbdeployer info defaults field-name [flags]
    
    Examples:
    
    	$ dbdeployer info defaults master-slave-base-port 
    
    
    Flags:
      -h, --help   help for defaults
    
    
    $ dbdeployer info version -h
    Displays the latest version available for deployment.
    If a short version is indicated (such as 5.7, or 8.0), only the versions belonging to that short
    version are searched.
    If "all" is indicated after the short version, displays all versions belonging to that short version.
    
    Usage:
      dbdeployer info version [short-version|all] [all] [flags]
    
    Examples:
    
        # Shows the latest version available
        $ dbdeployer info version
        8.0.16
    
        # shows the latest version belonging to 5.7
        $ dbdeployer info version 5.7
        5.7.26
    
        # shows the latest version for every short version
        $ dbdeployer info version all
        5.0.96 5.1.73 5.5.53 5.6.41 5.7.26 8.0.16
    
        # shows all the versions for a given short version
        $ dbdeployer info version 8.0 all
        8.0.11 8.0.12 8.0.13 8.0.14 8.0.15 8.0.16
    
    
    Flags:
      -h, --help   help for version
    
    

## remote
    $ dbdeployer remote -h
    Manages remote tarballs
    
    Usage:
      dbdeployer remote [command]
    
    Available Commands:
      download    download a remote tarball into a local file
      list        list remote tarballs
    
    Flags:
      -h, --help   help for remote
    
    
    $ dbdeployer remote download -h
    If no file name is given, the file name will be <version>.tar.xz
    
    Usage:
      dbdeployer remote download version [file-name] [flags]
    
    Aliases:
      download, get
    
    Flags:
      -h, --help                help for download
          --progress            Show download progress
          --progress-step int   Progress interval (default 10485760)
    
    
    $ dbdeployer remote list -h
    list remote tarballs
    
    Usage:
      dbdeployer remote list [version] [flags]
    
    Aliases:
      list, index
    
    Flags:
      -h, --help   help for list
    
    

## sandboxes
    $ dbdeployer sandboxes -h
    Lists all sandboxes installed in $SANDBOX_HOME.
    If sandboxes are installed in a different location, use --sandbox-home to 
    indicate where to look.
    Alternatively, using --catalog will list all sandboxes, regardless of where 
    they were deployed.
    
    Usage:
      dbdeployer sandboxes [flags]
    
    Aliases:
      sandboxes, installed, deployed
    
    Flags:
          --catalog     Use sandboxes catalog instead of scanning directory
          --flavor      Shows flavor in sandbox list
          --full-info   Shows all info in table format
          --header      Shows header with catalog output
      -h, --help        help for sandboxes
          --table       Shows sandbox list as a table
    
    

## unpack
    $ dbdeployer unpack -h
    If you want to create a sandbox from a tarball (.tar.gz or .tar.xz), you first need to unpack it
    into the sandbox-binary directory. This command carries out that task, so that afterwards 
    you can call 'deploy single', 'deploy multiple', and 'deploy replication' commands with only 
    the MySQL version for that tarball.
    If the version is not contained in the tarball name, it should be supplied using --unpack-version.
    If there is already an expanded tarball with the same version, a new one can be differentiated with --prefix.
    
    Usage:
      dbdeployer unpack MySQL-tarball [flags]
    
    Aliases:
      unpack, extract, untar, unzip, inflate, expand
    
    Examples:
    
        $ dbdeployer unpack mysql-8.0.4-rc-linux-glibc2.12-x86_64.tar.gz
        Unpacking tarball mysql-8.0.4-rc-linux-glibc2.12-x86_64.tar.gz to $HOME/opt/mysql/8.0.4
    
        $ dbdeployer unpack --prefix=ps Percona-Server-5.7.21-linux.tar.gz
        Unpacking tarball Percona-Server-5.7.21-linux.tar.gz to $HOME/opt/mysql/ps5.7.21
    
        $ dbdeployer unpack --unpack-version=8.0.18 --prefix=bld mysql-mybuild.tar.gz
        Unpacking tarball mysql-mybuild.tar.gz to $HOME/opt/mysql/bld8.0.18
    	
    
    Flags:
          --flavor string           Defines the tarball flavor (MySQL, NDB, Percona Server, etc)
      -h, --help                    help for unpack
          --overwrite               Overwrite the destination directory if already exists
          --prefix string           Prefix for the final expanded directory
          --shell                   Unpack a shell tarball into the corresponding server directory
          --target-server string    Uses a different server to unpack a shell tarball
          --unpack-version string   which version is contained in the tarball
          --verbosity int           Level of verbosity during unpack (0=none, 2=maximum) (default 1)
    
    

## usage
    $ dbdeployer usage -h
    Shows syntax and examples of tools installed in database sandboxes.
    
    Usage:
      dbdeployer usage [single|multiple] [flags]
    
    Flags:
      -h, --help   help for usage
    
    

## versions
    $ dbdeployer versions -h
    List available versions
    
    Usage:
      dbdeployer versions [flags]
    
    Aliases:
      versions, available
    
    Flags:
          --by-flavor       Shows versions list by flavor
          --flavor string   Get only versions of the given flavor
      -h, --help            help for versions
    
    
