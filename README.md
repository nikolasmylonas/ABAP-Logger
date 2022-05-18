# ABAP Logger

SAP Logging as painless as any other language.

ABAP Version: 702 or higher

See the [mission statement](docs/MISSION.md) 

## Features
  * Record message in [Application Log(BC-SRV-BAL)](https://help.sap.com/viewer/10a06f346c531014a346f3874a7621fd/7.0.38/en-US/4e21012c35d44180e10000000a15822b.html)
  * Display message

## Installation

- Install this project via [ABAPGit](http://abapgit.org).

**:warning: Migration Required :warning:**

On 2021, February 28 the folder logic was changed, and the abapGit may not able to perform this migration automatically. Therefore, you may need to follow the following steps:
1. Uninstall Repository (see [Uninstall repository](https://docs.abapgit.org/guide-online-uninstall.html)).
2. Reinstall ABAP-Logger (see:
   - online: see  [Install Online Repo](https://docs.abapgit.org/guide-online-install.html).
   - offline: see  [Install Offline Repo](https://docs.abapgit.org/guide-offline-install.html).

## Run Unit Tests
1. In transaction code SLG0, create the Subobject `LOGGER` for Object `ABAPUNIT`. 
2. Launch unit test with `Ctrl` + `Alt` + `F10` 


  
Application logs various log formats. #108 #71

This change displays different log formats as explained in the SAP demo program SBAL_DEMO_04. also it allows to set default context and display context fields in the log.

Changes in zif_logger
METHOD zif_logger->set_default_context and zif_logger->get_default_context.
new methods : used to set default context so that no need to pass context with every logged message.
METHOD zif_logger->fullscreen.
changes : display log as per display profile and context
METHOD zif_logger->add.
change : update context table name
METHOD zif_logger->export_to_table_with_context
change : export table with context
Changes in settings class
zif_logger_settings->set_context_tabname and zif_logger_settings->get_context_tabname.
new method : to capture context table name

zif_logger_settings->set_display_profile and zif_logger_settings->get_display_profile.
new method : to capture display profile and profile name.

get_standard_display_profile
new method : to get standard display profile using FM used 'BAL_DSP_PROFILE_STANDARD_GET'

get_no_tree_display_profile
new method : to get Fullscreen / no_tree display profile using FM used 'BAL_DSP_PROFILE_NO_TREE_GET'

get_single_display_profile
new method : to get single display profile using FM used 'BAL_DSP_PROFILE_SINGLE_LOG_GET'

get_self_display_profile
new method : to get user defined display profile

get_fcat_fm_context_tab
new method : to fill message field catlog with context fields using context table name.

Demo program test screen shots
demo program Selection.
image

o Single Display log (Program ZDEMO_LOGGER04_SINGLE)
image

o Standard Display log (program ZDEMO_LOGGER04_STANDARD)
image

o Display without a tree (Program ZDEMO_LOGGER04_NO_TREE) - Fullscreen
image

o Display select defined (Program ZDEMO_LOGGER04_self)
image

o Display export table with context tab(Program zdemo_logger_export_contextab)
