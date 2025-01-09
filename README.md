# Montana CAMA Database Extraction

## Requirements

This utility requires docker and docker-compose.

### <inline style="color:red">**_WARNING_**: </inline>The zipped STATE-WIDE file is >1.5GB and the unzipped Output.mdf is >9GB so be sure that your disk has plenty of free space. The total file size taken by the .mdf file and the output CSVs is >16GB.

### Linux

Follow directions found at https://docs.docker.com/compose/install/linux/ for your distribution.

### Mac

https://docs.docker.com/desktop/setup/install/mac-install/

## Usage

Download and extract Output.mdf from the zipped file found at http://ftpgeoinfo.msl.mt.gov/Data/Spatial/MSDI/Cadastral/ORION_SQLDatabases/STATE-WIDE.ZIP (see warning in Requirements above.)

Once the file has been extracted to the MDF directory, from the root directory where docker-compose.yaml is located, run:

```bash
# you may need to run with sudo priveleges
docker-compose up

```

After the database has been created and attached the utility will start to output csv files in the CSV folder. Once complete, in the terminal you will see:

```bash
All scripts have been executed. Waiting for MS SQL(pid ) to terminate.

```

While the container is still running, you can connect to the database using SSMS with the user `sa` and password `LocalPassword123!`.

And you can close the utility with Ctrl-C. Finally,

```bash
# you may need to run with sudo priveleges
docker-compose down
```

## Output

The utility will spit out a bunch of csv files into the CSV directory. The CSV's have been passed through sed to remove the MS SQL Server query formating in the header. The queries are run with NOCOUNT to also remove the query output at the bottom of the file.

## Clean Up

When done using the utility, it is suggested to delete all files in the MDF directory so that there is no confusion on future runs. The Output.mdf file and the montana_cama_log.ldf file are linked, such that you need both to rebuild the same database.
