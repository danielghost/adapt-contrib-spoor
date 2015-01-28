adapt-contrib-spoor
===================
Tracking plugin for the Adapt Framework. Currently (officially) only supports SCORM 1.2

##Installation
First, be sure to install the [Adapt Command Line Interface](https://github.com/adaptlearning/adapt-cli), then from the command line run:-
```
adapt install adapt-contrib-spoor
```

This component can also be installed by adding the component to the adapt.json file before running `adapt install`:
```
"adapt-contrib-spoor": "*"
```

##Usage instructions
You will need to add the JSON that is in [example.json](example.json) to your course.json, amending the settings as required.

In order to get this to work in adapt_framework, your course will need have tracking IDs added to blocks.json - this can be done by running
```
$ grunt tracking-insert
```

##Settings overview
 
A complete example of this components settings can be found in the [example.json](/adaptlearning/adapt-contrib-spoor/blob/master/example.json) file.

##Settings explained
####_isEnabled
If set to `true`, the plugin will try to connect to a SCORM conformant LMS on course launch and perform tracking. If you wish to switch off tracking without uninstalling the plugin - for example when testing locally with no LMS present - set this to `false`.

####_tracking
This section lists completion criteria and other tracking features such as whether to save a score back to the LMS or not.

#####_requireCourseCompleted
If set to `true`, the plugin will require that the user must complete all the components in the course (as well as any other completion criteria) before the course can be marked as finished in the LMS. 
Note that if this setting and `_requireAssessmentPassed` (see below) are both set to `true`, the user must pass the course assessment as well as complete all components in order to meet the completion criteria.

####_requireAssessmentPassed
If set to `true`, the plugin will require that the user pass the course assessment before the course can be marked as finished in the LMS. 
Note that if this setting and `_requireCourseCompleted` are both set to `true`, the user must complete all the components in the course as well as pass the assessment in order to meet the completion criteria.

####_shouldSubmitScore
If set to `true`, the score attained in any assessment will be reported back to the LMS (regardless of whether the user passes or fails the assessment).

####_reporting
Defines what status to report back to the LMS

#####_onTrackingCriteriaMet
What status to report back to the LMS when the tracking criteria are met. 
Valid values are: 'completed', 'passed', 'failed', and 'incomplete' (note - these must be lowercase). 
Under most circumstances, if you are tracking a course by assessment, you would set this to 'passed'. Otherwise 'completed' is the usual value to use.

#####_onAssessmentFailure
What status to report back to the LMS when the assessment is failed. 
Some Learning Management Systems will prevent the user from making further attempts at the course after it has been set to 'failed', it's therefore common to set this to 'incomplete' to allow the user more attempts to pass the assessment.

#####References
This plugin uses the excellent :sparkles: [pipwerks SCORM API Wrapper](https://github.com/pipwerks/scorm-api-wrapper/) for JavaScript :sparkles: