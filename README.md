# serviceability-zeep-samples

## Overview

Sample scripts demonstrating use of the Python Zeep SOAP library with the CUCM Serviceability APIs.

[https://developer.cisco.com/site/sxml/](https://developer.cisco.com/site/sxml/)

## Available samples

* `perfmonPort_collect_counter_data.py` - Demonstrates retrieving and parsing performance counter data via the `<perfmonCollectCounterData>` request

## Getting started

* Install Python 3.7

  (On Windows, choose the option to add to PATH environment variable)

* The project was built/tested using [Visual Studio Code](https://code.visualstudio.com/)

* Dependency Installation:

    ```bash
    pip install -r requirements.txt
    ```
  
* Edit `creds.py` to specify your CUCM address and [Serviceability API user credentials](https://d1nmyq4gcgsfi5.cloudfront.net/site/sxml/help/faq/#sec-1)

* The Serviceability SOAP API WSDL files for CUCM v12.5 are included in this project.  If you'd like to use a different version, replace the files in `schema/` with the versions from your CUCM, which can be retrieved at:

    * CDRonDemand: `https://{cucm}/CDRonDemandService2/services/CDRonDemandService?wsdl`

    * Log Collection: `https://{cucm}:8443/logcollectionservice2/services/LogCollectionPortTypeService?wsdl`

    * PerfMon: `https://{cucm}:8443/perfmonservice2/services/PerfmonService?wsdl`

    * RisPort70: `https://{cucm}:8443/realtimeservice2/services/RISService70?wsdl`

    * Control Center Services:
        `https://ServerName:8443/controlcenterservice2/services/ControlCenterServices?wsdl`
        `https://ServerName:8443/controlcenterservice2/services/ControlCenterServicesEx?wsdl`

* To run a specific sample, in Visual Studio Code open the sample `.py` file you want to run, then press `F5`, or open the Debugging panel and click the green 'Launch' arrow

## Hints

* You can get a 'dump' of an API WSDL to see how Zeep interprets it, for example by running (Mac/Linux):

    ```bash
    python3 -mzeep schema/PerfmonService.wsdl > wsdl.txt
    ```

    This can help with identifying the proper object structure to send to Zeep

* Elements which contain a list, such as:

    ```xml
    <members>
        <member>
            <subElement1/>
            <subElement2/>
        </member>
        <member>
            <subElement1/>
            <subElement2/>
        </member>
    </members>
    ```

    are represented a little differently than expected by Zeep.  Note that `<member>` becomes an array, not `<members>`:

    ```python
    {
        'members': {
            'member': [
                {
                    'subElement1': 'value',
                    'subElement2': 'value'
                },
                {
                    'subElement1': 'value',
                    'subElement2': 'value'
                }
            ]
        }
    }
    ```
