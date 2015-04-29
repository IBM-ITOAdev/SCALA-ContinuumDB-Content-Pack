# IBM SmartCloud Analytics - Log Analysis Pack for ingesting data from ContinuumDB

# Description
This pack contains content to	extract	data from ContinuumDB (	Alarts,	Actions	and Error tables) and ingest them into Log Analytics

# What is included

1. A sample logstash configuration file **(continuum.conf)** to connect to a ContinuumDB and extract data from 3 tables
2. Custom DSV Content Pack properties files to create CSV based SCALA source types for the following:
   - ContinuumActivityEvent.props
   - ContinuumAlarmEvent.props
   - ContinuumErrorEvent.props

# Deploying the Content Pack

1. Install logstash 
2. Install genjdbc plugin (Available here [genjdbc](https://github.com/IBM-ITOAdev/logstash-input-genjdbc) )
3. Ensure that you have MSSQL database driver **jdbcsql4.jar** available in your environment
4. Review the sample logstash configuration file **(continuum.conf)** and change/set as appropriate the various entries
   1. jdbcHost and jdbcPort  
   2. jdbcUser/jdbcPassword
   3. path to .pstore files 
   4. jdbcDriverPath
   5. scala_url, scala_user, scala_password
   6. disk_cache_path
7. This example configuration will only work with the upcoming release of the SCALA-Logstash Integration. If you do not have this contact Doug McClure for assistance
8. Copy the 3 DSV Pack properties files into the $SCALAHOME/unity_content/DSVToolkit_v1.1.0.3 directory
9. Edit each DSV Pack properties file and update the scalaHome directory path.
10.  From the $SCALAHOME/unity_content/DSVToolkit_v1.1.0.3 directory, execute this command to build and deploy each DSV Content Pack you plan on using into SCALA: python dsvGen.py [FILENAME].props -d -f -u unityadmin -p unityadmin
11. Create SCALA datasources which use the new DSV Content Pack source types that you have deployed for each SCALA log type. Be sure to set the host and path values to match what you're setting in your logstash configuration. 
12. Start up logstash and verify logs are being consumed properly. Watch for activity in logstash stdout or within SCALA search results.

# Need Help

This is a community contributed content pack and no explicit support, guarantee or warranties are provided by IBM nor the contributor. Feel free to engage the community on the ITOAdev forum if you need help!