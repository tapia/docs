.. _conan_conf:

conan.conf
==========

The typical location of the **conan.conf** file is the directory ``~/.conan/``:

.. code-block:: text

    [log]
    run_to_output = True        # environment CONAN_LOG_RUN_TO_OUTPUT
    run_to_file = False         # environment CONAN_LOG_RUN_TO_FILE
    level = critical            # environment CONAN_LOGGING_LEVEL
    # trace_file =              # environment CONAN_TRACE_FILE
    print_run_commands = False  # environment CONAN_PRINT_RUN_COMMANDS

    [general]
    default_profile = default
    compression_level = 9                 # environment CONAN_COMPRESSION_LEVEL
    sysrequires_sudo = True               # environment CONAN_SYSREQUIRES_SUDO
    request_timeout = 60                  # environment CONAN_REQUEST_TIMEOUT (seconds)
    default_package_id_mode = semver_direct_mode # environment CONAN_DEFAULT_PACKAGE_ID_MODE
    # parallel_download = 8               # experimental download binaries in parallel
    # full_transitive_package_id = 0
    # retry = 2                           # environment CONAN_RETRY
    # retry_wait = 5                      # environment CONAN_RETRY_WAIT (seconds)
    # sysrequires_mode = enabled          # environment CONAN_SYSREQUIRES_MODE (allowed modes enabled/verify/disabled)
    # vs_installation_preference = Enterprise, Professional, Community, BuildTools # environment CONAN_VS_INSTALLATION_PREFERENCE
    # verbose_traceback = False           # environment CONAN_VERBOSE_TRACEBACK
    # error_on_override = False           # environment CONAN_ERROR_ON_OVERRIDE
    # bash_path = ""                      # environment CONAN_BASH_PATH (only windows)
    # read_only_cache = True              # environment CONAN_READ_ONLY_CACHE
    # cache_no_locks = True               # environment CONAN_CACHE_NO_LOCKS
    # user_home_short = your_path         # environment CONAN_USER_HOME_SHORT
    # use_always_short_paths = False      # environment CONAN_USE_ALWAYS_SHORT_PATHS
    # skip_vs_projects_upgrade = False    # environment CONAN_SKIP_VS_PROJECTS_UPGRADE
    # non_interactive = False             # environment CONAN_NON_INTERACTIVE
    # skip_broken_symlinks_check = False  # enviornment CONAN_SKIP_BROKEN_SYMLINKS_CHECK
    # revisions_enabled = False           # environment CONAN_REVISIONS_ENABLED

    # conan_make_program = make           # environment CONAN_MAKE_PROGRAM (overrides the make program used in AutoToolsBuildEnvironment.make)
    # conan_cmake_program = cmake         # environment CONAN_CMAKE_PROGRAM (overrides the make program used in CMake.cmake_program)

    # cmake_generator                     # environment CONAN_CMAKE_GENERATOR
    # cmake_generator_platform            # environment CONAN_CMAKE_GENERATOR_PLATFORM
    # http://www.vtk.org/Wiki/CMake_Cross_Compiling
    # cmake_toolchain_file                # environment CONAN_CMAKE_TOOLCHAIN_FILE
    # cmake_system_name                   # environment CONAN_CMAKE_SYSTEM_NAME
    # cmake_system_version                # environment CONAN_CMAKE_SYSTEM_VERSION
    # cmake_system_processor              # environment CONAN_CMAKE_SYSTEM_PROCESSOR
    # cmake_find_root_path                # environment CONAN_CMAKE_FIND_ROOT_PATH
    # cmake_find_root_path_mode_program   # environment CONAN_CMAKE_FIND_ROOT_PATH_MODE_PROGRAM
    # cmake_find_root_path_mode_library   # environment CONAN_CMAKE_FIND_ROOT_PATH_MODE_LIBRARY
    # cmake_find_root_path_mode_include   # environment CONAN_CMAKE_FIND_ROOT_PATH_MODE_INCLUDE

    # msbuild_verbosity = minimal         # environment CONAN_MSBUILD_VERBOSITY

    # cpu_count = 1             # environment CONAN_CPU_COUNT

    # Change the default location for building test packages to a temporary folder
    # which is deleted after the test.
    # temp_test_folder = True             # environment CONAN_TEMP_TEST_FOLDER

    # cacert_path                         # environment CONAN_CACERT_PATH
    # scm_to_conandata                    # environment CONAN_SCM_TO_CONANDATA

    # config_install_interval = 1h
    # required_conan_version = >=1.26

    # keep_python_files = False           # environment CONAN_KEEP_PYTHON_FILES

    [storage]
    # This is the default path, but you can write your own. It must be an absolute path or a
    # path beginning with "~" (if the environment var CONAN_USER_HOME is specified, this directory, even
    # with "~/", will be relative to the conan user home, not to the system user home)
    path = ./data
    # download_cache = /path/to/my/cache

    [proxies]
    # Empty (or missing) section will try to use system proxies.
    # As documented in https://requests.readthedocs.io/en/master/user/advanced/#proxies - but see below
    # for proxies to specific hosts
    # http = http://user:pass@10.10.1.10:3128/
    # http = http://10.10.1.10:3128
    # https = http://10.10.1.10:1080
    # To specify a proxy for a specific host or hosts, use multiple lines each specifying host = proxy-spec
    # http =
    #   hostname.to.be.proxied.com = http://user:pass@10.10.1.10:3128
    # You can skip the proxy for the matching (fnmatch) urls (comma-separated)
    # no_proxy_match = *bintray.com*, https://myserver.*

    [hooks]    # environment CONAN_HOOKS
    attribute_checker

    # Default settings now declared in the default profile

Log
+++

The ``level`` variable, defaulted to 50 (critical events), declares the LOG level .
If you want to show more detailed logging information, set this variable to lower values,
as 10 to show debug information, or use the level names as ``critical``, ``error``, ``warning``,
``info`` and ``debug``. You can also adjust the environment variable ``CONAN_LOGGING_LEVEL``.
The level number is related to the `Python Logging Levels`_.

The ``print_run_commands``, when is 1, Conan will print the executed commands in ``self.run`` to the output.
You can also adjust the environment variable CONAN_PRINT_RUN_COMMANDS

The ``run_to_file`` variable, defaulted to False, will print the output from the ``self.run``
executions to the path that the variable specifies.
You can also adjust the environment variable ``CONAN_LOG_RUN_TO_FILE``.

The ``run_to_output`` variable, defaulted to 1, will print to the ``stdout`` the output from the
``self.run`` executions in the conanfile. You can also adjust the environment variable ``CONAN_LOG_RUN_TO_OUTPUT``.

The ``trace_file`` variable enable extra logging information about your conan command executions.
Set it with an absolute path to a file.
You can also adjust the environment variable ``CONAN_TRACE_FILE``.

General
+++++++

The ``vs_installation_preference`` variable determines the preference of usage when searching a Visual installation. The order of preference
by default is Enterprise, Professional, Community and BuildTools. It can be fixed to just one type of installation like only BuildTools. You
can also adjust the environment variable ``CONAN_VS_INSTALLATION_PREFERENCE``.

The ``verbose_traceback`` variable will print the complete traceback when an error occurs in a recipe or even in the conan code base, allowing
to debug the detected error.

The ``error_on_override`` turn the messages related to dependencies overriding into errors. When a downstream
package overrides some dependency upstream, if this variable is ``True`` then an error will be raised; to bypass
these errors those requirements should be declared explicitly with the ``override`` keyword.

The ``bash_path`` variable is used only in windows to help the
:ref:`tools.run_in_windows_bash()<tools_run_in_windows_bash>` function to locate our Cygwin/MSYS2 bash.
Set it with the bash executable path if it's not in the PATH or you want to use a different one.

The ``cache_no_locks`` variable is used to disable locking mechanism of local cache.
This is primary used for debugging purposes, and in general it's not recommended to disable locks otherwise,
as it may result in corrupted packages.

The ``default_package_id_mode`` changes the way package IDs are computed. By default, if not specified
it will be ``semver_direct_mode``, but can change to any value defined in :ref:`package_id_mode`.

The ``full_transitive_package_id`` changes the way package IDs are computed regarding transitive dependencies.
By default, if not specified will be disabled (``0``). Read more about it in :ref:`full_transitive_package_id`.

The ``parallel_download`` configuration defines the number of threads to be used to do parallel downloads of
different binaries. This happens when dependencies are installed (``conan install``, ``conan create``) and when
multiple binaries for the same package are retrieved via ``conan download`` command. This is an **experimental**
feature, subject to change. It is known that the output is still not clean, and will be mangled when using multiple
threads. Please report on https://github.com/conan-io/conan/issues about performance gains, and other issues.
You might want to try this one in combination with the ``storage.download_cache`` configuration (see below.)

The ``revisions_enabled`` variable controls the package revisioning feature. See :ref:`package_revisions` for more info`

The ``cmake_***`` variables will declare the corresponding CMake variable when you use the
:ref:`cmake generator<cmake_generator>` and the :ref:`CMake build tool<cmake_reference>`.


The ``msbuild_verbosity`` variable is used only by :ref:`MSBuild<msbuild>` and :ref:`CMake<cmake_reference>` build helpers.
For the :ref:`CMake<cmake_reference>` build helper, it has an effect only for ```Visual Studio``` generators.
Variable defines verbosity level used by the ```msbuild``` tool, as documented on `MSDN <https://docs.microsoft.com/en-us/visualstudio/msbuild/msbuild-command-line-reference?view=vs-2017>`.
By default, ```minimal`` verbosity level is used, matching the Visual Studio IDE behavior.
Allowed values are (in ascending order): ```quiet```, ```minimal```, ```normal```, ```detailed```, ```diagnostic```.
You can also adjust the environment variable ``CONAN_MSBUILD_VERBOSITY``.

The ``conan_make_program`` variable used by :ref:`CMake<cmake_reference>` and :ref:`AutotoolsBuildEnvironment <autotools_reference>` build helpers.
It overrides a default ```make``` executable, might be useful in case you need to use a different make (e.g. BSD Make instead of GNU Make, or MinGW Make).
Set it with the make executable path if it's not in the PATH or you want to use a different one.

The ``conan_cmake_program`` variable used only by :ref:`CMake<cmake_reference>` build helper.
It overrides a default ```cmake``` executable, might be useful in case you need to use a CMake wrapper tool (such as scan build).
Set it with the cmake executable path if it's not in the PATH or you want to use a different one.

The ``cpu_count`` variable set the number of cores that the :ref:`tools_cpu_count` will return,
by default the number of cores available in your machine.
Conan recipes can use the ``cpu_count()`` tool to build the library using more than one core.

The ``retry`` variable allows to set up the global default value for the number of retries in all commands related to
download/upload. User can override the value provided by the variable if the command provides an argument with the same name.

The ``retry_wait`` variable allows to set up the global default value for the time (in seconds) to wait until the next retry
on failures in all commands related to download/upload. User can override the value provided by the variable if the command provides
an argument with the same name.

The ``sysrequires_mode`` variable, defaulted to ``enabled`` (allowed modes ``enabled/verify/disabled``)
controls whether system packages should be installed into the system via ``SystemPackageTool`` helper,
typically used in :ref:`method_system_requirements`.
You can also adjust the environment variable ``CONAN_SYSREQUIRES_MODE``.

The ``sysrequires_sudo`` variable, defaulted to True, controls whether ``sudo`` is used for installing apt, yum, etc.
system packages via ``SystemPackageTool``. You can also adjust the environment variable ``CONAN_SYSREQUIRES_SUDO``.


The ``request_timeout`` variable, defaulted to 30 seconds, controls the time after Conan will stop waiting for a response.
Timeout is not a time limit on the entire response download; rather, an exception is raised if the server has not issued a
response for timeout seconds (more precisely, if no bytes have been received on the underlying socket for timeout seconds).
If no timeout is specified explicitly, it do not timeout.

The ``user_home_short`` specify the base folder to be used with the :ref:`short paths<short_paths_reference>` feature.
If not specified, the packages marked as `short_paths` will be stored in the ``C:\.conan`` (or the current drive letter).

If the variable is set to "None" will disable the `short_paths` feature in Windows,
for modern Windows that enable long paths at the system level.

Setting this variable equal to, or to a subdirectory of, the local conan cache (e.g. ~/.conan)
would result in an invalid cache configuration and is therefore disallowed.

The ``verbose_traceback`` variable will print the complete traceback when an error occurs in a recipe or even
in the conan code base, allowing to debug the detected error.

The ``cacert_path`` variable lets the user specify a custom path to the *cacert.pem* file to use
in requests. You can also adjust this value using the environment variable ``CONAN_CACERT_PATH``.

The ``client_cert_path`` and ``client_cert_key_path`` variables let the user specify a custom path to the :ref:`client_certificates` files.

The ``scm_to_conandata`` variable tells Conan to store the resolved information of the :ref:`SCM feature<scm_feature>` in the
:ref:`conandata.yml<conandata_yml>` file instead of modifying the recipe file itself. You can also adjust
this value using the environment variable ``CONAN_SCM_TO_CONANDATA``.

The ``skip_broken_symlinks_check`` variable (defaulted to ``False``) allows the existence broken symlinks while creating a package.

The ``config_install_interval`` variable starts a time scheduler which runs :command:`conan config install` according the time interval
configured. It only accepts the follow time intervals: seconds, minutes, hours, days and weeks (e.g 10s, 35m, 48h, 1d, 2w). Empty units or not listed units are not valid, they are considered an error and will be removed automatically on the next execution.

The ``required_conan_version`` variable validates if the current Conan client version is valid according to its version. When it's not
according to the required version or its range, Conan raises an exception before running any command. It accepts SemVer format, including version range.
This configuration is useful when a company wants to align the Conan client version used by all teams. This can be also specified at
:ref:`recipe level<conanfile_required_version>` if you need adding this information just for certain recipes.

The ``keep_python_files`` variable will allow Python *.pyc* files to be packaged. If set to ``True``,
*.pyc* files will be added to the Conan package, otherwise they will be filtered.

Storage
+++++++

The ``storage.path`` variable define the path where all the packages will be stored. By default it is *./data*, which
is relative to the folder containing this *conan.conf* file, which by default is the *<userhome>/.conan* folder.
It can start with "~", and that will be expanded to the current user home folder. If the environment var CONAN_USER_HOME is specified,
the "~" will be replaced by the current Conan home (the folder pointed by the CONAN_USER_HOME environment variable).


On Windows:

- It is recommended to assign it to some unit, e.g. map it to X: in order to avoid hitting the 260 chars path name length limit).
- Also see the :ref:`short_paths docs<short_paths_reference>` to know more about how to mitigate the limitation of 260 chars path name length limit.
- It is recommended to disable the Windows indexer or exclude the storage path to avoid problems (busy resources).

.. note::

    If you want to change the default "conan home" (directory where ``conan.conf`` file is) you can adjust
    the environment variable ``CONAN_USER_HOME``.


The ``storage.download_cache`` variable defines the path to a folder that can be used to cache the different file downloads from Conan servers but
also from user downloads via the ``tools.get()`` and ``tools.download()`` methods that provide a checksum. Defining this variable will both configure
the path and activate the download cache. If it is not defined, the download cache will not be used.

Read more about the :ref:`download cache here <download_cache>`.

.. _proxys:

Proxies
+++++++

.. warning::

    ``no_proxy`` is deprecated in favor of ``no_proxy_match`` since Conan 1.16.

If you leave the ``[proxies]`` section blank or delete the section, conan will copy the system
configured proxies, but if you configured some exclusion rule it won't work:

.. code-block:: text

    [proxies]
    # Empty (or missing) section will try to use system proxies.

You can specify http and https proxies as follows. Use the `no_proxy_match` keyword to specify a list
of URLs or patterns that will skip the proxy:

.. code-block:: text

    [proxies]
    # As documented in https://requests.readthedocs.io/en/master/user/advanced/#proxies
    http: http://user:pass@10.10.1.10:3128/
    http: http://10.10.1.10:3128
    https: http://10.10.1.10:1080
    http: http://10.10.2.10
        hostname1.to.be.proxied.com = http://user:pass@10.10.3.10
        hostname2.to.be.proxied.com = http://user:pass@10.10.4.10
    no_proxy_match: http://url1, http://url2, https://url3*, https://*.custom_domain.*

Use `http=None` and/or `https=None` to disable the usage of a proxy.

To nominate a proxy for a specific scheme and host only, add `host.to.proxy=` in front of the url of the proxy
(the `host.to.proxy` name must exactly match the host name that should be proxied). You can list
several `host name = proxy` pairs on separate indented lines.

You can still specify a default proxy, without a host, which will be
used if none of the host names match. If you do not, then the proxy is disabled for non-matching hosts.

If this fails, you might also try to set environment variables:

.. code-block:: bash

   # linux/osx
   $ export HTTP_PROXY="http://10.10.1.10:3128"
   $ export HTTPS_PROXY="http://10.10.1.10:1080"

   # with user/password
   $ export HTTP_PROXY="http://user:pass@10.10.1.10:3128/"
   $ export HTTPS_PROXY="http://user:pass@10.10.1.10:3128/"

   # windows (note, no quotes here)
   $ set HTTP_PROXY=http://10.10.1.10:3128
   $ set HTTPS_PROXY=http://10.10.1.10:1080

.. _`Python Logging Levels`: https://docs.python.org/3/library/logging.html#logging-levels
