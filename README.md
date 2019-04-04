#### Set up intelliJ IDEA:
- [ ] folow the instructions &nbsp; https://wiki.v-env.net/display/TBODEV/IntelliJ+IDEA
#### Win Win Git repository:
- [ ] clone the repo &nbsp; [Win Win Services BitBucket Repository](https://bitbucket.v-env.net/scm/tbo/winwin-services.git)

#### Win Win Setup
- [ ] folow the instructions &nbsp; https://wiki.v-env.net/display/DMTBWWT/WinWin+Service+-+Setup+Development++Environment
#### Instructions for IntelliJ and Git
https://wiki.v-env.net/display/DMTBWWT/Using+GIT+over+IntelliJe+IDE

#### Git
- [ ] install git
- if you don't wan't to use IntelliJ's Git support install Git GUI you like

#### Java
- [ ] install  jdk1.8.0_191

#### Create folder for maven related files 
- [ ] download and unzip maven, put settings.xml in conf folder (file can be found on Win Win instalation page)
- [ ] add folder for maven repository (used for both projects)

#### Tbo Win Win Config (contains configuration for Core services)
- [ ] unzip WINWIN_CONFIG_DATA.7z 
- [ ] DIMA-GROUP-IT-TBO folder exists
- [ ] DIMA-OUTLET-IT-TBO folder exists
- [ ] change IP address and hostname in files in both folders (_tbo.system.xml_)
- [ ] change path for log files in files in both folders (_xml logging files_)
- [ ] check if you changed all IP address, hostnames and paths

#### Database
- [ ] install OracleXE 
- [ ] run these commands after database installation has finished:
> create user winadmin_test identified by "secret";
  create user win_outlet_test identified by "secret";
  create user tbo_core identified by "secret";
  create user outlet_core identified by "secret";

> grant connect, resource, create view to winadmin_test;
  grant connect, resource, create view to win_outlet_test;
  grant connect, resource, create view to tbo_core;
  grant connect, resource, create view to outlet_core;
  
> create tablespace DATA datafile 'C:\oraclexe\app\oracle\oradata\XE\data01.dbf' size 100m autoextend on next 10m maxsize      unlimited;

- [ ] check if username for database user is coresponding to username in files named tbo.system.properties
*additional _create session grant_ may be necessary*

#### Import in IntelliJ
- [ ] checkout development branch
- [ ] check if you have access to &nbsp; http://tbonexus.v-ls.local
- [ ] follow instructions on Wiki page

## Run Configurations in IntelliJ
##### Country
- [ ] add to VM options (change the path to your config folder):
 `-Dtbo.system.properties=/home/denis/TboWinWinConf/WINWIN_CONFIG_DATA/TboConfig/tbo.system.properties`
##### Outlet
- [ ] add to VM options (change the path to your config folder):
`-Dtbo.system.properties= /home/denis/TboWinWinConf/WINWIN_CONFIG_DATA/TboConfigOutlet/tbo.system.properties -Dtbo.container.name="denis-XPS-8700"`
##### WRMI
- [ ] if already not present add wrmi to **tbo.system.xml** like this:
    ```xml 
    <tbo:service>
        <tbo:type>wrmi</tbo:type>
        <tbo:hostName>denis-XPS-8700</tbo:hostName>
    </tbo:service>
    ```
- check if WRMI is running on https://localhost:8081/ login: rooty/rooty
## Known errors

> **Hash code error** 
Can be fixed with git settings: git config --global core.autocrlf false 

> **There is no service context available for service 10:desktop-XPS-8700/wrmi/1**
Check data in table SYS_COUNTRY_SERVER and username in *settings.xml* and *tbo.system.properties*
Check if WRMI project is add as resource to ServiceManager project
