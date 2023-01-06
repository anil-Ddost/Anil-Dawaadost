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
    # Project ID for this request.
    project = res[3]

    # The name of the zone for this request.
    zone = res[1]

    # Name of the instance resource to stop.
    instance = res[0]  

    request = service.instances().delete(project=project, zone=zone, instance=instance)
    response = request.execute()

    pprint(response)
