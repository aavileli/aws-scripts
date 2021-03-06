# cfn-show #

The cfn-show command provides a number of different views of a CloudFormation json
templates contents.

The basic command will display all the names of all resources in a given
section, defaulting to 'Resources'.

    $ cfn-show templates/web-app.json

    LocationAppServerELB
    AWS::ElasticLoadBalancing::LoadBalancer

    LocationAppServerFleet
    AWS::AutoScaling::AutoScalingGroup

    LocationAppServerFleetLaunchConfig
    AWS::AutoScaling::LaunchConfiguration


You can also specify an alternate section to display.

    $ cfn-show templates/web-app.json outputs

    HTTPSURL
    Outputs


If you are unsure of which sections a template contains you can run

    $ cfn-show templates/web-app.json sections

    Conditions
    Mappings
    Outputs
    Parameters
    Resources


Once you've found the section and resource you're interested in
you can expand it -


    $ cfn-show templates/web-app.json resources IAMRolesStack

    {
        "Type": "AWS::CloudFormation::Stack",
        "Properties": {
            "TemplateURL": {
                "Ref": "IAMRolesURL"
            },
            "Parameters": {
                "App": "location",
                "Type": "webapp",
                "Stack": {
                    "Ref": "CommonStackName"
                },
                "Env": {
                    "Ref": "DeploymentEnvironment"
                }
            }
        }
    }
    

You can alter the format of this display with the 'indent' and 'show name'
options:

    $ cfn-show templates/web-app.json resources IAMRolesStack -n -i 2

    "IAMRolesStack" :  {
      "Type": "AWS::CloudFormation::Stack",
      "Properties": {
        "TemplateURL": {
          "Ref": "IAMRolesURL"
        },
      ... snip ...



