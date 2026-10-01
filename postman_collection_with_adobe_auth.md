{
	"info": {
		"_postman_id": "fdec3833-b35a-499f-b11e-db947b52eb53",
		"name": "AEM-Naehas-Disclosure (With Auto Auth)",
		"schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json",
		"_exporter_id": "46297566"
	},
	"variable": [
		{
			"key": "imsEndpoint",
			"value": "ims-na1.adobelogin.com",
			"type": "string"
		},
		{
			"key": "clientId",
			"value": "",
			"type": "string"
		},
		{
			"key": "clientSecret",
			"value": "",
			"type": "string"
		},
		{
			"key": "technicalAccountId",
			"value": "",
			"type": "string"
		},
		{
			"key": "orgId",
			"value": "",
			"type": "string"
		},
		{
			"key": "privateKey",
			"value": "",
			"type": "string"
		},
		{
			"key": "metaScopes",
			"value": "",
			"type": "string"
		}
	],
	"item": [
		{
			"name": "Push disclosure - EN",
			"event": [
				{
					"listen": "prerequest",
					"script": {
						"exec": [
							"// Pre-request Script: Fetch JWT Access Token from Adobe IMS",
							"const imsEndpoint = pm.variables.get('imsEndpoint') || 'ims-na1.adobelogin.com';",
							"const clientId = pm.variables.get('clientId');",
							"const clientSecret = pm.variables.get('clientSecret');",
							"const technicalAccountId = pm.variables.get('technicalAccountId');",
							"const orgId = pm.variables.get('orgId');",
							"const privateKey = pm.variables.get('privateKey');",
							"const metaScopes = pm.variables.get('metaScopes');",
							"",
							"// Optional: If using Client Credentials grant / OAuth token endpoint",
							"const tokenUrl = `https://${imsEndpoint}/ims/token/v2`;",
							"",
							"// Request token if clientId is provided in variables",
							"if (clientId && clientSecret) {",
							"    pm.sendRequest({",
							"        url: tokenUrl,",
							"        method: 'POST',",
							"        header: {",
							"            'Content-Type': 'application/x-www-form-urlencoded'",
							"        },",
							"        body: {",
							"            mode: 'urlencoded',",
							"            urlencoded: [",
							"                { key: 'grant_type', value: 'client_credentials' },",
							"                { key: 'client_id', value: clientId },",
							"                { key: 'client_secret', value: clientSecret },",
							"                { key: 'scope', value: metaScopes }",
							"            ]",
							"        }",
							"    }, function (err, res) {",
							"        if (err) {",
							"            console.error('Error fetching token:', err);",
							"        } else {",
							"            const data = res.json();",
							"            if (data.access_token) {",
							"                pm.environment.set('bearerToken', data.access_token);",
							"                console.log('Access token generated successfully');",
							"            }",
							"        }",
							"    });",
							"}"
						],
						"type": "text/javascript",
						"packages": {}
					}
				}
			],
			"request": {
				"auth": {
					"type": "bearer",
					"bearer": [
						{
							"key": "token",
							"value": "{{bearerToken}}",
							"type": "string"
						}
					]
				},
				"method": "PUT",
				"header": [
					{
						"key": "Authorization",
						"value": "Bearer {{bearerToken}}",
						"type": "text",
						"disabled": true
					}
				],
				"body": {
					"mode": "raw",
					"raw": "{\r\n   \"disclosureContent\": \"{\\\"Standard_Fields\\\":{\\\"createdby\\\":\\\"James Maher\\\",\\\"createdon\\\":\\\"Aug 5, 2026\\\",\\\"disclosureCode\\\":\\\"TEST30.01.01.01\\\",\\\"expirationdate\\\":\\\"\\\",\\\"naehas_internal_id\\\":\\\"27338\\\",\\\"permDisclosureDisplayTitle\\\":\\\"TEST30.01.01.01ENG-MDC End to End Test Core Disclosure\\\",\\\"status\\\":\\\"Available\\\",\\\"statusupdatedby\\\":\\\"James Maher\\\",\\\"statusupdatedon\\\":\\\"Aug 10, 2026\\\",\\\"type\\\":\\\"Disclosure Language\\\",\\\"updatedby\\\":\\\"James Maher\\\",\\\"updatedon\\\":\\\"Aug 10, 2026\\\",\\\"version\\\":\\\"2\\\"},\\\"disclosure_language_lifecycle\\\":{\\\"attestation_date\\\":\\\"2026-08-06 00:00\\\",\\\"compliance_review_date\\\":\\\"2026-08-06 00:00\\\",\\\"compliance_reviewer\\\":\\\"Other\\\",\\\"compliance_reviewer_other\\\":\\\"TEST REVIEWER II\\\",\\\"lcr_review_source\\\":\\\"Aprimo,ASG Compliance,CAR,Email,ERISA,Naehas,Red Oak,WFII Compliance\\\",\\\"legal_review_date\\\":\\\"2026-08-06 00:00\\\",\\\"legal_reviewer\\\":\\\"Other\\\",\\\"legal_reviewer_other\\\":\\\"TEST REVIEWER I\\\",\\\"next_legal_review_date\\\":\\\"2028-08-06\\\",\\\"recertification_start_date\\\":\\\"2028-04-06\\\",\\\"review_source_id\\\":\\\"TEST RS ID\\\"},\\\"inherited_data\\\":{\\\"LastModifiedDateTimestamp\\\":\\\"Aug 10, 2026\\\",\\\"additional_information\\\":\\\"More MDC tracking info\\\",\\\"core_disclosure_version\\\":\\\"2\\\",\\\"disclosure_audience\\\":\\\"Acquisition,Auto Lending - Consumer,Auto Lending - Dealer,Existing Customer,Home Lending - Consumer,Home Lending - Trade,Internal,Merchant\\\",\\\"displayTitleId\\\":\\\"TEST30.01.01.01ENG-MDC End to End Test Core Disclosure\\\",\\\"how_to_use\\\":\\\"HOW TO USE THIS TEST DISCLOSURE\\\",\\\"language_code\\\":\\\"ENG\\\",\\\"placement\\\":\\\"Body Copy,Footnote,Header,Other,Script\\\",\\\"placement_other\\\":\\\"TEST PLACEMENT\\\",\\\"product\\\":\\\"Adjustable-rate mortgage (ARM),Affordability Calculator,Agency 97,Asset Secured Lending Wells Fargo Prime Line of Credit,Business Payroll Services,BusinessLine line of credit,Choice Privileges Mastercard,Choice Privileges Select Mastercard,Clear Access Banking,Commercial Equity Loan,Commercial Purchase Loan,Commercial Refinance Loan,Credit Close Up,Dealer,Debt Optimizer,Down payment Assistance Program (DAP),Dream Plan Home,Everyday Checking,FHA,FICO,Financial Health,Fixed rate mortgage,General Deposits,Initiate Business Checking,Jumbo/Non-Conforming Loans,Low to Moderate Income (LMI),Mastercard Access Card,My Mortgage Gift,Navigate Business Checking,Neighborhood LIFT,One Key Mastercard,One Key+ Mastercard,Online Mortgage App (OMA),Optimize Business Checking,Other,Platinum Savings,Preferred Payment Plan  auto payment,Premier Checking,Prime Checking,Priority Buyer Preapproval,Private Label,Relocation loans,Signify Business Cash Mastercard,Signify Business Elite Mastercard,Signify Business Essential Mastercard,Small Business Administration,Small Business Advantage line of credit,Student/Teen Checking,The Private Bank By Invitation Visa Signature card,Union Plus,VA,Way2Save Savings,Wells Fargo Active Cash Visa,Wells Fargo Advisors By Invitation Visa Signature card,Wells Fargo Advisors Premium Rewards Visa Signature card,Wells Fargo Attune World Elite Mastercard,Wells Fargo Autograph Card,Wells Fargo Autograph Journey Visa Card,Wells Fargo Cash Back card,Wells Fargo Cash Back Visa Signature card,Wells Fargo Cash Wise Visa Platinum card,Wells Fargo Cash Wise Visa Signature card,Wells Fargo Cash Wise World Elite Mastercard,Wells Fargo CDs,Wells Fargo Funding (WFF),Wells Fargo Home Rebate card,Wells Fargo Home Rebate Visa Signature card,Wells Fargo Personal Loan,Wells Fargo Platinum Mastercard,Wells Fargo Platinum Visa,Wells Fargo Premier Autograph Visa Infinite,Wells Fargo Prime Line of Credit,Wells Fargo Private Bank Visa Infinite,Wells Fargo Reflect Visa,Wells Fargo Rewards card,Wells Fargo Visa Signature card,Wells Fargo Works,Youth Banking\\\",\\\"product_other\\\":\\\"TEST PRODUCT\\\",\\\"r_disclosure_prefix_language\\\":\\\"TEST\\\",\\\"r_test_asset_indicator_language\\\":\\\"Yes\\\",\\\"trigger_words\\\":\\\"MDC, Reusable, Consumable\\\"},\\\"language_information\\\":{\\\"associated_english_id\\\":\\\"\\\",\\\"base_title_description\\\":\\\"MDC End to End Test Core Disclosure\\\",\\\"channel\\\":\\\"ATM,Branch,Digital,E-Mail,Internal Content,Media,Other,Print,TV/Radio\\\",\\\"channel_other\\\":\\\"TEST CHANNEL\\\",\\\"disclosure_core_assigned_to\\\":\\\"TEST30.01.01\\\",\\\"language\\\":\\\"English\\\",\\\"marketing_tactic\\\":\\\"Digital Audio/Radio or Traditional Radio,Digital Video,Mobile,OOH,TV\\\"},\\\"permutationConditions\\\":[],\\\"resolvedModularTexts\\\":[{\\\"disclosureResolvedText\\\":\\\"More content for TEST30 disclosure\\\"},{\\\"resolvedBackTranslation\\\":\\\"\\\"}],\\\"translation\\\":{\\\"translation_request_id\\\":\\\"\\\"}}\",\r\n   \"subfolder\": \"CRD\",\r\n   \"pushRequestId\": \"s5783-64798-jf9939\",\r\n   \"metas\": []\r\n}",
					"options": {
						"raw": {
							"language": "json"
						}
					}
				},
				"url": {
					"raw": "",
					"protocol": "https",
					"host": [
						"",
						"adobeaemcloud",
						"com"
					],
					"path": [
						"content",
						"api",
						"v1",
						"disclosures"
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
				"type": "text/javascript",
				"exec": [
					""
				]
			}
		},
		{
			"listen": "test",
			"script": {
				"type": "text/javascript",
				"exec": [
					""
				]
			}
		}
	]
}
