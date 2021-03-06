# Deploy three NIC Citrix ADC HA solution using Google Deployment Manager
You can now deploy a Citrix ADC HA solution on Google Cloud Platform (GCP).  A high availability (HA) deployment of two NetScaler appliances can provide uninterrupted operation in any transaction. With one appliance configured as the primary node and the other as the secondary node, the primary node accepts connections and manages servers while the secondary node monitors the primary. If, for any reason, the primary node is unable to accept connections, the secondary node takes over.

## Introduction
This template deploys a Citrix HA solution with two instance with three NICs each. Each NIC handles management, client, and server traffic respectively.

### Prerequisites
1. A subscription to Google Cloud Platform.
2. Install [Google SDK](https://cloud.google.com/sdk/install) to access the "gcloud" utility.
3. Citrix ADC BYOL license based on your requirements.
4. Three network and three subnets within the networks under VPC Network in the same or different availability zones.
5. A Citrix ADC image on Google Cloud Platform.
 	1. For marketplace image, please refer to the table below.
	2. Details to create a custom image image can be found [here](https://docs.citrix.com/en-us/netscaler/12-1/deploying-vpx/deploy-vpx-google-cloud.html).

### Citrix ADC Images

## BYOL
| Release | Image Name | Project Name | URL |
| --- | --- | --- | --- |
| `13.0` | nsvpx-gcp-13-0-36-102-public | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/nsvpx-gcp-13-0-36-102-public |
| `13.0` | citrix-adc-vpx-byol-13-0-41-25 | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/citrix-adc-vpx-byol-13-0-41-25 |
| `13.0` | citrix-adc-vpx-byol-13-0-latest | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/citrix-adc-vpx-byol-13-0-latest |

## Express License
| Release | Image Name | Project Name | URL |
| --- | --- | --- | --- |
| `13.0` | citrix-adc-vpx-express-13-0-41-25 | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/citrix-adc-vpx-express-13-0-41-25 |
| `13.0` | citrix-adc-vpx-express-13-0-latest | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/citrix-adc-vpx-express-13-0-latest |

## Standard Licence
| Release | Image Name | Project Name | URL |
| --- | --- | --- | --- |
| `13.0` | citrix-adc-vpx-10-standard-13-0-41-25 | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/citrix-adc-vpx-10-standard-13-0-41-25 |
| `13.0` | citrix-adc-vpx-10-standard-13-0-latest | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/citrix-adc-vpx-10-standard-13-0-latest |

## Platinum License
| Release | Image Name | Project Name | URL |
| --- | --- | --- | --- |
| `13.0` | citrix-adc-vpx-10-platinum-13-0-41-25 | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/citrix-adc-vpx-10-platinum-13-0-41-25 |
| `13.0` | citrix-adc-vpx-10-platinum-13-0-latest | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/citrix-adc-vpx-10-platinum-13-0-latest |

## Enterprise License
| Release | Image Name | Project Name | URL |
| --- | --- | --- | --- |
| `13.0` | citrix-adc-vpx-10-enterprise-13-0-41-25 | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/citrix-adc-vpx-10-enterprise-13-0-41-25 |
| `13.0` | citrix-adc-vpx-10-enterprise-13-0-latest | citrix-master-project | https://www.googleapis.com/compute/v1/projects/citrix-master-project/global/images/citrix-adc-vpx-10-enterprise-13-0-latest |

### Deploy a Citrix ADC HA solution
You would find three files under this directory. A YAML configuration file, a Python template, and a schema. Note the following points before you start.

1.	Ensure you meet the prerequisites given in the "Prerequisites" section.
2.	Edit the configuration.yml file.
	1.  Refer to the template.py.schema file to understand the variables(keys) present in the YAML file.
	2.	Populate/edit the variables (keys) present in the configuration.yml file to suite your needs.
3.	Deploy the Citrix ADC HA instances
	1.	Use the following command to deploy the instance.<br>
	    gcloud deployment-manager deployments create <deployment_name> --config configuration.yml
	2.	For more information refer https://cloud.google.com/deployment-manager/docs/
4.	View the outputs (The Citrix ADC HA instance parameters). Use the following commands to view the instance that include the external/internal IPs of the primary and secondary.
	1.	Run the command,<br>
	    gcloud deployment-manager deployments describe <deployment_name> | grep manifest:
	2.	Fetch the manifest ID from the output of the above command.<br>
	    Example: manifest: manifest-1542970019879
	3.	Run the following command.<br>
	    gcloud deployment-manager manifests describe <manifest_id> --deployment <deployment_name> --format="value(layout)"
	4.	In the output, under the outputs section the details regarding the Citrix ADC primary and secondary nodes, specifically the internal/external IPs can be found.

## Troubleshooting
1.	Refer to the template.py.schema file to make sure the variables types are adhered to while editing configuration.yml.
2.	Make sure all the values within configuration.yml are placed within double quotes.
3.	There might be possible indentation errors while editing the configuration files or the python template if it was opened with an intention to edit.
