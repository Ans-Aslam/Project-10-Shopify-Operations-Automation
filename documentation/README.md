# Project 10 Architecture

## Overview

Project 10 is a modular Shopify Operations Automation System built with n8n.

Instead of placing all business operations into one large workflow, the system is divided into six specialized workflows.

## Workflow Architecture


                         SHOPIFY
                            |
          +-----------------+-----------------+
          |                 |                 |
          v                 v                 v
      10-A Orders      10-B Fulfillment   10-C Inventory
          |                 |                 |
          +-----------------+-----------------+
                            |
                     SHOPIFY OPERATIONS
                            |
                +-----------+-----------+
                |                       |
                v                       v
           10-D Refunds          10-E Daily Report
                |                       |
                +-----------+-----------+
                            |
                            v
                   10-F Error Handler

## **Workflow Modules**

**10-A — Order Automation**

Handles Shopify order-related automation.

Main responsibilities:

•	Receive order events 

•	Process order information 

•	Validate order data 

•	Send customer/order notifications 

•	Log order information 

•	Handle workflow failures 

**10-B — Fulfillment Automation**

Handles fulfillment and shipping-related operations.

Main responsibilities:

•	Process fulfillment events 

•	Extract fulfillment information 

•	Process tracking information 

•	Send operational notifications 

•	Handle workflow failures 

**10-C — Inventory Monitoring**

Monitors Shopify inventory and identifies stock conditions requiring attention.

Main responsibilities:

•	Retrieve product inventory 

•	Monitor available stock 

•	Compare stock against thresholds 

•	Identify low-stock products 

•	Identify critical-stock products 

•	Maintain an Inventory Audit Log 

•	Send alerts 

**10-D — Refund Automation**

Handles Shopify refund-related operations.

Main responsibilities:

•	Process refund events 

•	Prepare refund information 

•	Determine refund details 

•	Record operational information 

•	Send notifications 

•	Handle workflow failures 

**10-E — Daily Reporting**

Generates a daily operational report.

The report includes:

•	Total Products 

•	Healthy Products 

•	Low Products 

•	Critical Products 

•	Total Units Sold 

•	Average Daily Sales 

•	Total Available Stock 

The report can be stored in Google Sheets and distributed through Slack.

**10-F — Centralized Error Handler**

Provides centralized error handling for Project 10.

The individual workflows can pass failure information to the centralized error workflow.

Main responsibilities:

•	Receive workflow error information

•	Identify the failed workflow

•	Process error details

•	Provide operational visibility

•	Send Slack error notifications

## **Integrations**

**System**	             |            **Role**

Shopify	                            
E-commerce platform and operational data

n8n	                                 
Automation orchestration

Google Sheets	                       
Audit logging and reporting

Slack	                               
Operational and error notifications

Webhooks	                          
Event-driven triggers

APIs	                               
System integration

JSON	                               
Data exchange

## **Architecture Principles**

**Modular Design**

Each business function is implemented as a separate workflow.

This makes the system easier to:

•	Maintain 

•	Debug 

•	Test 

•	Extend 

•	Reuse 

**Centralized Error Handling**

Workflow failures are routed toward a centralized error-handling process rather than requiring completely independent error-management logic in every workflow.

**Event-Driven Automation**

Shopify events can trigger operational workflows automatically.

**Scheduled Automation**

The daily reporting workflow runs on a scheduled basis to provide regular operational visibility.

**Testing**

The six workflows were connected and tested end-to-end.

Testing covered:

•	Order processing 

•	Fulfillment processing 

•	Inventory monitoring 

•	Refund processing 

•	Daily reporting 

•	Error handling 

•	Inter-workflow communication 

**Security**

The public GitHub repository contains sanitized workflow exports.

Production credentials and secrets are intentionally excluded.

Examples include:

•	API keys 

•	Access tokens 

•	Client secrets 

•	OAuth credentials 

•	Webhook secrets 

•	Passwords 

•	Private environment variables
                            |
                            v
                          SLACK
