{
	"info": {
		"_postman_id": "49ff3ea0-180b-4c2d-b949-6eaa1e008e22",
		"name": "Nutanix REST API Testing",
		"description": "Example Postman collection containing basic Nutanix REST API requests.",
		"schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
	},
	"item": [
		{
			"name": "v1",
			"item": [
				{
					"name": "/vms",
					"item": [
						{
							"name": "API v1 - Get VM Stats",
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "Content-Type",
										"value": "application/json",
										"type": "text"
									}
								],
								"url": {
									"raw": "https://{{cluster_ip}}:9440/PrismGateway/services/rest/v1/vms/{{vm_uuid}}/stats/?startTimeInUsecs={{start_time_in_usecs}}&endTimeInUsecs={{end_time_in_usecs}}&metrics={{vm_metric}}&intervalInSecs={{interval}}",
									"protocol": "https",
									"host": [
										"{{cluster_ip}}"
									],
									"port": "9440",
									"path": [
										"PrismGateway",
										"services",
										"rest",
										"v1",
										"vms",
										"{{vm_uuid}}",
										"stats",
										""
									],
									"query": [
										{
											"key": "startTimeInUsecs",
											"value": "{{start_time_in_usecs}}"
										},
										{
											"key": "endTimeInUsecs",
											"value": "{{end_time_in_usecs}}"
										},
										{
											"key": "metrics",
											"value": "{{vm_metric}}"
										},
										{
											"key": "intervalInSecs",
											"value": "{{interval}}"
										}
									]
								}
							},
							"response": []
						}
					],
					"protocolProfileBehavior": {},
					"_postman_isSubFolder": true
				}
			],
			"protocolProfileBehavior": {}
		},
		{
			"name": "v2.0",
			"item": [
				{
					"name": "/vms",
					"item": [
						{
							"name": "API v2.0 - List all VMs",
							"protocolProfileBehavior": {
								"disableBodyPruning": true
							},
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "Content-Type",
										"value": "application/json",
										"type": "text"
									}
								],
								"body": {
									"mode": "raw",
									"raw": ""
								},
								"url": {
									"raw": "https://{{cluster_ip}}:9440/api/nutanix/v2.0/vms",
									"protocol": "https",
									"host": [
										"{{cluster_ip}}"
									],
									"port": "9440",
									"path": [
										"api",
										"nutanix",
										"v2.0",
										"vms"
									]
								}
							},
							"response": []
						}
					],
					"protocolProfileBehavior": {},
					"_postman_isSubFolder": true
				},
				{
					"name": "/storage_containers",
					"item": [
						{
							"name": "API v2.0 - Get storage container information",
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "Content-Type",
										"type": "text",
										"value": "application/json"
									}
								],
								"url": {
									"raw": "https://{{cluster_ip}}:9440/api/nutanix/v2.0/storage_containers/{{container_uuid}}",
									"protocol": "https",
									"host": [
										"{{cluster_ip}}"
									],
									"port": "9440",
									"path": [
										"api",
										"nutanix",
										"v2.0",
										"storage_containers",
										"{{container_uuid}}"
									]
								},
								"description": "This request can be used to get information about a specific storage container in a specific cluster."
							},
							"response": []
						}
					],
					"protocolProfileBehavior": {},
					"_postman_isSubFolder": true
				}
			],
			"protocolProfileBehavior": {}
		},
		{
			"name": "v3",
			"item": [
				{
					"name": "/batch",
					"item": [
						{
							"name": "API v3 - Batch Request (Simple)",
							"request": {
								"method": "POST",
								"header": [
									{
										"key": "Content-Type",
										"value": "application/json",
										"type": "text"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"action_on_failure\": \"CONTINUE\",\n    \"execution_order\": \"SEQUENTIAL\",\n    \"api_request_list\": [\n        {\n            \"operation\": \"POST\",\n            \"path_and_params\": \"/api/nutanix/v3/vms\",\n            \"body\": {\n                \"spec\": {\n                    \"name\": \"vm_from_batch\",\n                    \"resources\": {}\n                },\n                \"metadata\": {\n                    \"kind\": \"vm\"\n                }\n            }\n        },\n        {\n            \"operation\": \"POST\",\n            \"path_and_params\": \"/api/nutanix/v3/images\",\n            \"body\": {\n                \"spec\": {\n                    \"name\": \"image_from_batch\",\n                    \"resources\": {\n                        \"image_type\": \"DISK_IMAGE\",\n                        \"source_uri\": \"https://cloud.centos.org/centos/7/images/CentOS-7-x86_64-GenericCloud-1905.qcow2\"\n                    },\n                    \"description\": \"Image created via v3 API batch request\"\n                },\n                \"api_version\": \"3.1.0\",\n                \"metadata\": {\n                    \"kind\": \"image\",\n                    \"categories\": {},\n                    \"name\": \"image_from_batch\"\n                }\n            }\n        }\n    ],\n    \"api_version\": \"3.0\"\n}"
								},
								"url": {
									"raw": "https://{{pc_ip}}:9440/api/nutanix/v3/batch",
									"protocol": "https",
									"host": [
										"{{pc_ip}}"
									],
									"port": "9440",
									"path": [
										"api",
										"nutanix",
										"v3",
										"batch"
									]
								}
							},
							"response": []
						}
					],
					"protocolProfileBehavior": {},
					"_postman_isSubFolder": true
				},
				{
					"name": "/images",
					"item": [
						{
							"name": "API v3 - Create Image From URL",
							"request": {
								"method": "POST",
								"header": [
									{
										"key": "Content-Type",
										"value": "application/json",
										"type": "text"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"spec\": {\n        \"name\": \"image_from_v3_api\",\n        \"resources\": {\n            \"image_type\": \"DISK_IMAGE\",\n            \"source_uri\": \"https://cloud.centos.org/centos/7/images/CentOS-7-x86_64-GenericCloud-1905.qcow2\"\n        },\n        \"description\": \"Image created via v3 API batch request\"\n    },\n    \"api_version\": \"3.1.0\",\n    \"metadata\": {\n        \"kind\": \"image\",\n        \"categories\": {},\n        \"name\": \"image_from_batch_04\"\n    }\n}"
								},
								"url": {
									"raw": "https://{{pc_ip}}:9440/api/nutanix/v3/images",
									"protocol": "https",
									"host": [
										"{{pc_ip}}"
									],
									"port": "9440",
									"path": [
										"api",
										"nutanix",
										"v3",
										"images"
									]
								}
							},
							"response": []
						}
					],
					"protocolProfileBehavior": {},
					"_postman_isSubFolder": true
				},
				{
					"name": "/vms",
					"item": [
						{
							"name": "API v3 - List First 100 VMs",
							"event": [
								{
									"listen": "test",
									"script": {
										"id": "a57d226c-059a-48ca-b1ef-28954992c2f0",
										"exec": [
											""
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "POST",
								"header": [
									{
										"key": "Content-Type",
										"type": "text",
										"value": "application/json"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"kind\": \"vm\",\n    \"length\": 100\n}"
								},
								"url": {
									"raw": "https://{{pc_ip}}:9440/api/nutanix/v3/vms/list",
									"protocol": "https",
									"host": [
										"{{pc_ip}}"
									],
									"port": "9440",
									"path": [
										"api",
										"nutanix",
										"v3",
										"vms",
										"list"
									]
								},
								"description": "Use Prism API v3 to list all available networks.  This can be useful when gathering network UUIDs for use with future API requests e.g. create VM"
							},
							"response": []
						},
						{
							"name": "API v3 - Create VM (Detailed)",
							"event": [
								{
									"listen": "prerequest",
									"script": {
										"id": "f50aea15-1e26-4574-8e2c-4cdc46516449",
										"exec": [
											"var vm_name = pm.variables.get(\"vm_name\");",
											"var cluster_uuid = pm.variables.get(\"cluster_uuid\");",
											"var cluster_name = pm.variables.get(\"cluster_name\");",
											"",
											"postman.setEnvironmentVariable(\"vm_name\", vm_name)",
											"postman.setEnvironmentVariable(\"cluster_name\", cluster_name)",
											"postman.setEnvironmentVariable(\"cluster_uuid\", cluster_uuid)"
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "POST",
								"header": [
									{
										"key": "Content-Type",
										"type": "text",
										"value": "application/json"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n\t\"spec\":{\n\t\t\"name\": \"{{vm_name}}\",\n\t\t\"resources\":{\n\t\t\t\"power_state\":\"ON\",\n\t\t\t\"num_vcpus_per_socket\":1,\n\t\t\t\"num_sockets\":1,\n\t\t\t\"memory_size_mib\":1024,\n\t\t\t\"disk_list\":[{\n\t\t\t\t\"disk_size_mib\":1024,\n\t\t\t\t\"device_properties\":{\n\t\t\t\t\t\"device_type\":\"DISK\"\n\t\t\t\t}\n\t\t\t},\n\t\t\t{\n\t\t\t\t\"device_properties\":{\n\t\t\t\t\t\"device_type\":\"CDROM\"\n\t\t\t\t}\n\t\t\t}]\n\t\t},\n\t\t\"cluster_reference\":{\n\t\t\t\"kind\":\"cluster\",\n\t\t\t\"name\":\"{{cluster_name}}\",\n\t\t\t\"uuid\":\"{{cluster_uuid}}\"\n\t\t}\n\t},\n\t\"api_version\":\"3.1.0\",\n\t\"metadata\":{\n\t\t\"kind\":\"vm\"\n\t}\n}"
								},
								"url": {
									"raw": "https://{{pc_ip}}:9440/api/nutanix/v3/vms",
									"protocol": "https",
									"host": [
										"{{pc_ip}}"
									],
									"port": "9440",
									"path": [
										"api",
										"nutanix",
										"v3",
										"vms"
									]
								},
								"description": "Use Prism API v3 to list all available networks.  This can be useful when gathering network UUIDs for use with future API requests e.g. create VM"
							},
							"response": []
						},
						{
							"name": "API v3 - Delete VM (BE CAREFUL!)",
							"request": {
								"method": "DELETE",
								"header": [
									{
										"key": "Content-Type",
										"value": "application/json",
										"type": "text"
									}
								],
								"body": {
									"mode": "raw",
									"raw": ""
								},
								"url": {
									"raw": "https://{{pc_ip}}:9440/api/nutanix/v3/vms/{{vm_uuid}}",
									"protocol": "https",
									"host": [
										"{{pc_ip}}"
									],
									"port": "9440",
									"path": [
										"api",
										"nutanix",
										"v3",
										"vms",
										"{{vm_uuid}}"
									]
								}
							},
							"response": []
						},
						{
							"name": "API v3 - Update VM (BE CAREFUL!)",
							"event": [
								{
									"listen": "prerequest",
									"script": {
										"id": "98da8d46-07ed-4568-8dd2-4a56107b4232",
										"exec": [
											"var vm_name = pm.variables.get(\"container_uuid\");",
											"var cluster_uuid = pm.variables.get(\"cluster_uuid\");",
											"var cluster_name = pm.variables.get(\"cluster_name\");",
											"",
											"postman.setEnvironmentVariable(\"vm_name\", vm_name)",
											"postman.setEnvironmentVariable(\"cluster_name\", cluster_name)",
											"postman.setEnvironmentVariable(\"cluster_uuid\", cluster_uuid)"
										],
										"type": "text/javascript"
									}
								}
							],
							"request": {
								"method": "PUT",
								"header": [
									{
										"key": "Content-Type",
										"value": "application/json",
										"type": "text"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"spec\": {\n        \"name\": \"{{vm_name}}\",\n        \"resources\": {\n            \"num_threads_per_core\": 1,\n            \"vnuma_config\": {\n                \"num_vnuma_nodes\": 0\n            },\n            \"serial_port_list\": [],\n            \"nic_list\": [],\n            \"num_vcpus_per_socket\": 1,\n            \"num_sockets\": 2,\n            \"enable_cpu_passthrough\": false,\n            \"gpu_list\": [],\n            \"is_agent_vm\": false,\n            \"memory_size_mib\": 1024,\n            \"boot_config\": {\n                \"boot_device_order_list\": [\n                    \"CDROM\",\n                    \"DISK\",\n                    \"NETWORK\"\n                ],\n                \"boot_type\": \"LEGACY\"\n            },\n            \"hardware_clock_timezone\": \"UTC\",\n            \"disable_branding\": false,\n            \"power_state\": \"OFF\",\n            \"power_state_mechanism\": {\n                \"guest_transition_config\": {\n                    \"should_fail_on_script_failure\": false,\n                    \"enable_script_exec\": false\n                },\n                \"mechanism\": \"HARD\"\n            },\n            \"vga_console_enabled\": true,\n            \"disk_list\": []\n        },\n        \"cluster_reference\": {\n            \"kind\": \"cluster\",\n            \"name\": \"{{cluster_name}}\",\n            \"uuid\": \"{{cluster_uuid}}\"\n        }\n    },\n    \"api_version\": \"3.1\"\n}"
								},
								"url": {
									"raw": "https://{{pc_ip}}:9440/api/nutanix/v3/vms/{{vm_uuid}}",
									"protocol": "https",
									"host": [
										"{{pc_ip}}"
									],
									"port": "9440",
									"path": [
										"api",
										"nutanix",
										"v3",
										"vms",
										"{{vm_uuid}}"
									]
								}
							},
							"response": []
						}
					],
					"event": [
						{
							"listen": "prerequest",
							"script": {
								"id": "b60b3281-7a17-484a-9328-561c16a46d2a",
								"type": "text/javascript",
								"exec": [
									""
								]
							}
						},
						{
							"listen": "test",
							"script": {
								"id": "7c066bdc-5e07-46ea-b6a6-89e9ac6e666d",
								"type": "text/javascript",
								"exec": [
									""
								]
							}
						}
					],
					"protocolProfileBehavior": {},
					"_postman_isSubFolder": true
				}
			],
			"protocolProfileBehavior": {}
		}
	],
	"auth": {
		"type": "basic",
		"basic": [
			{
				"key": "password",
				"value": "{{password}}",
				"type": "string"
			},
			{
				"key": "username",
				"value": "{{username}}",
				"type": "string"
			}
		]
	},
	"event": [
		{
			"listen": "prerequest",
			"script": {
				"id": "b52c8896-af12-4bfa-970a-e51a24824829",
				"type": "text/javascript",
				"exec": [
					""
				]
			}
		},
		{
			"listen": "test",
			"script": {
				"id": "c83a19ec-3de3-4d92-bd4f-3f2393cfd786",
				"type": "text/javascript",
				"exec": [
					""
				]
			}
		}
	],
	"variable": [
		{
			"id": "698a8f86-0b83-4385-b34f-ca75892e81ad",
			"key": "centos8_uri",
			"value": "http://centos.mirror.ausnetservers.net.au/8.0.1905/isos/x86_64/CentOS-8-x86_64-1905-dvd1.iso",
			"type": "string"
		},
		{
			"id": "f3c2733a-1654-47e1-a35f-ee824af5818f",
			"key": "cluster_ip",
			"value": "",
			"type": "string"
		},
		{
			"id": "39045fdb-ec65-4fa0-9627-49d58b56e311",
			"key": "cluster_name",
			"value": "",
			"type": "string"
		},
		{
			"id": "12eeadbd-69c5-4e82-ac89-21899506f47d",
			"key": "cluster_uuid",
			"value": "",
			"type": "string"
		},
		{
			"id": "7e92bd15-1d8f-4fc5-983a-5481afd4150c",
			"key": "container_name",
			"value": "",
			"type": "string"
		},
		{
			"id": "ce31738b-65ef-4e2f-99d9-3805124606c2",
			"key": "container_uuid",
			"value": "",
			"type": "string"
		},
		{
			"id": "157d4dfd-fb10-40dd-b73a-4f2a8c2569ff",
			"key": "end_time_in_usecs",
			"value": "",
			"type": "string"
		},
		{
			"id": "aaab985b-e9b1-4ef8-9d61-7acf1d776a8b",
			"key": "interval",
			"value": "30",
			"type": "string"
		},
		{
			"id": "16d8ae51-5717-4b59-8e7f-025ad0d9f622",
			"key": "password",
			"value": "",
			"type": "string"
		},
		{
			"id": "7dd2ca57-bf70-48e8-93f1-1823e3821d5f",
			"key": "pc_ip",
			"value": "",
			"type": "string"
		},
		{
			"id": "416f35c2-3036-4bee-b829-7e5e648269a4",
			"key": "start_time_in_usecs",
			"value": "",
			"type": "string"
		},
		{
			"id": "17ef5d11-5073-4b4d-918a-a1c6e6f7d5e7",
			"key": "username",
			"value": "admin",
			"type": "string"
		},
		{
			"id": "51538d97-1a3d-4e7f-bfbc-6fb410f02bf4",
			"key": "vm_name",
			"value": "",
			"type": "string"
		},
		{
			"id": "031e4a65-9e31-4c30-999d-c7c0dfec61fa",
			"key": "vm_metric",
			"value": "hypervisor_cpu_usage_ppm",
			"type": "string"
		},
		{
			"id": "8ffe9839-17bf-4761-8422-da05557671a0",
			"key": "vm_uuid",
			"value": "",
			"type": "string"
		}
	],
	"protocolProfileBehavior": {}
}
