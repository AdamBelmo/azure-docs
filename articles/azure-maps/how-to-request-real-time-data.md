---
title: Request real-time public transit data with Microsoft Azure Maps Mobility services (Preview) 
description: Learn how to request real-time public transit data, such as arrivals at a transit stop. See how to use the Azure Maps Mobility services (Preview) for this purpose.
author: anastasia-ms
ms.author: v-stharr
ms.date: 06/23/2021
ms.topic: how-to
ms.service: azure-maps
services: azure-maps

ms.custom: mvc
---

# Request real-time public transit data using the Azure Maps Mobility services (Preview) 

> [!IMPORTANT]
> The Azure Maps Mobility Services Preview has been retired and will no longer be available and supported after October 5, 2021. All other Azure Maps APIs and Services are unaffected by this retirement announcement.
> For details, see [Azure Maps Mobility Preview Retirement](https://azure.microsoft.com/updates/azure-maps-mobility-services-preview-retirement/).


This article shows you how to use Azure Maps [Mobility services](/rest/api/maps/mobility) to request real-time public transit data.

In this article, you will learn how to request next real-time arrivals for all lines arriving at a given stop

## Prerequisites

You first need to have an Azure Maps account and a subscription key to make any calls to the Azure Maps public transit APIs. For information, follow instructions in [Create an account](quick-demo-map-app.md#create-an-azure-maps-account) to create an Azure Maps account. Follow the steps in [get primary key](quick-demo-map-app.md#get-the-primary-key-for-your-account) to obtain the primary key for your account. For more information on authentication in Azure Maps, see [manage authentication in Azure Maps](./how-to-manage-authentication.md).

This article uses the [Postman app](https://www.getpostman.com/apps) to build REST calls. You can use any API development environment that you prefer.

## Request real-time arrivals for a stop

In order to request real-time arrivals data of a particular public transit stop, you'll need to make request to the [Real-time Arrivals API](/rest/api/maps/mobility/getrealtimearrivalspreview) of the Azure Maps [Mobility Service (Preview)](/rest/api/maps/mobility). You'll need the **metroID** and **stopID** to complete the request. To learn more about how to request these parameters, see our guide on how to [request public transit routes](./how-to-request-transit-data.md).

Let's use "522" as our metro ID, which is the metro ID for the  "Seattle–Tacoma–Bellevue, WA" area. Use "522---2060603" as the stop ID, this bus stop is at "Ne 24th St & 162nd Ave Ne, Bellevue WA". To request the next five real-time arrivals data, for all next live arrivals at this stop, complete the following steps:

1. Open the Postman app. Select **New** to create the request. In the **Create New** window, select **HTTP Request**. Enter a **Request name** for the request.

2. Select the **GET** HTTP method on the builder tab and enter the following URL to create a GET request. Replace `{subscription-key}`, with your Azure Maps primary key.

    ```HTTP
    https://atlas.microsoft.com/mobility/realtime/arrivals/json?subscription-key={subscription-key}&api-version=1.0&metroId=522&query=522---2060603&transitType=bus
    ```

3. After a successful request, you'll receive the following response.  Notice that parameter 'scheduleType' defines whether the estimated arrival time is based on real-time or static data.

    ```JSON
    {
        "results": [
            {
                "arrivalMinutes": 8,
                "scheduleType": "realTime",
                "patternId": "522---4143196",
                "line": {
                    "lineId": "522---3760143",
                    "lineGroupId": "522---666077",
                    "direction": "backward",
                    "agencyId": "522---5872",
                    "agencyName": "Metro Transit",
                    "lineNumber": "249",
                    "lineDestination": "South Bellevue S Kirkland P&R",
                    "transitType": "Bus"
                },
                "stop": {
                    "stopId": "522---2060603",
                    "stopKey": "71300",
                    "stopName": "NE 24th St & 162nd Ave NE",
                    "stopCode": "71300",
                    "position": {
                        "latitude": 47.631504,
                        "longitude": -122.125275
                    },
                    "mainTransitType": "Bus",
                    "mainAgencyId": "522---5872",
                    "mainAgencyName": "Metro Transit"
                }
            },
            {
                "arrivalMinutes": 25,
                "scheduleType": "realTime",
                "patternId": "522---3510227",
                "line": {
                    "lineId": "522---2756599",
                    "lineGroupId": "522---666063",
                    "direction": "forward",
                    "agencyId": "522---5872",
                    "agencyName": "Metro Transit",
                    "lineNumber": "226",
                    "lineDestination": "Bellevue Transit Center Crossroads",
                    "transitType": "Bus"
                },
                "stop": {
                    "stopId": "522---2060603",
                    "stopKey": "71300",
                    "stopName": "NE 24th St & 162nd Ave NE",
                    "stopCode": "71300",
                    "position": {
                        "latitude": 47.631504,
                        "longitude": -122.125275
                    },
                    "mainTransitType": "Bus",
                    "mainAgencyId": "522---5872",
                    "mainAgencyName": "Metro Transit"
                }
            }
        ]
    }
    ```

## Next steps

Learn how to request transit data using Mobility services (Preview):

> [!div class="nextstepaction"]
> [How to request transit data](how-to-request-transit-data.md)

Explore the Azure Maps Mobility services (Preview) API documentation:

> [!div class="nextstepaction"]
> [Mobility services API documentation](/rest/api/maps/mobility)