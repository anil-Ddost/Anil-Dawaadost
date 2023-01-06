# Anil-Dawaadost
from pprint import pprint
import requests
from googleapiclient import discovery
from oauth2client.client import GoogleCredentials

def StopVm():
    credentials = GoogleCredentials.get_application_default()

    service = discovery.build('compute', 'v1', credentials=credentials)
    metadata_server = "http://metadata/computeMetadata/v1/instance/"
    metadata_flavor = {'Metadata-Flavor' : 'Google'}
    res =(requests.get(metadata_server + 'hostname', headers = metadata_flavor).text).split('.')
    # Project ID for this request.
    project = res[3]

    # The name of the zone for this request.
    zone = res[1]

    # Name of the instance resource to stop.
    instance = res[0]  

    request = service.instances().stop(project=project, zone=zone, instance=instance)
    response = request.execute()

    pprint(response)

def DeleteVm():
    credentials = GoogleCredentials.get_application_default()

    service = discovery.build('compute', 'v1', credentials=credentials)
    metadata_server = "http://metadata/computeMetadata/v1/instance/"
    metadata_flavor = {'Metadata-Flavor' : 'Google'}
    res =(requests.get(metadata_server + 'hostname', headers = metadata_flavor).text).split('.')
    
    -----------------------------------------------------------------------------------------------------
    Connect postgres by using Jupyter
    import pandas as pd
    import sqlite3
    pip install ipython-sql
    import pandas.io.sql as sqlio
    import psycopg2 as ps
    conn2 = ps.connect (dbname="postgres",
                    user ="postgres",
                    password ="Daw@@d0$t",
                    host="34.93.78.248",
                    port ="5432" )
    
    
    # Project ID for this request.
    
    __________________________________________________________________________________________________________
    
    
    project = res[3]

    # The name of the zone for this request.
    zone = res[1]

    # Name of the instance resource to stop.
    instance = res[0]  

    request = service.instances().delete(project=project, zone=zone, instance=instance)
    response = request.execute()

    pprint(response)
--------------------------------------------------------------------------------------------------------------------------
select id.c_br_code,id.c_year, id.c_prefix,id.n_srno, id.d_date,id.t_ltime, id.c_item_code,im.c_cat_code,id.n_disc_per, ims.n_total 
from 
inv_det id
inner join 
item_mst im
on 
im.c_code=id.c_item_code
inner join
inv_mst ims
on
ims.c_br_code=id.c_br_code and ims.c_prefix=id.c_prefix and ims.c_year=id.c_year and ims.n_srno=id.n_srno
where id.d_date=today() and im.c_cat_code='RX' and ims.n_total<50 and id.c_br_code in (select c_br_code from branch_group_det where c_code = 'bg0002') ;
