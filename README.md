# HA_DoneChecker
Homeassistant blueprint to regularily check if an action is preformed since it checked last time.

# Usecases:
* You want to have a check that your backup keeps running successfully
* You want a weekly reminder at a given time that the waste bin needs to be put outside for collection.
* You want an alarm if your server did not register that its alive
* you want a reminder to water the plants if you did not do it yet (e.g. put a NFS tag on the plant to confirm that it's been watered)


# What it does:
It checks daily/weekly at a given time if the action was registered to have been performed since the last check.

The confirmation of an action can be done via

* a call to a webhook (e.g. via a cronjob/end of the bash script you want to monitor using curl -X POST homeassistant:8123/api/webhook/NameOfReminder )
* manually changing the input variable in the HA interface
* using a NFC-tag. (the tag-id must be given by its ID)

If the task was
* NOT performed, it creates a persistent notification + optional actions
* performed since the last check (status of the input_boolean is off), it resets the input_boolean for the next check

# Setup
* As the blueprint cannot setup the required input_boolean, a input_boolean needs to be manually created bevorehand. In order to do this go to "Configuration" -> "Helpers" -> "+ ADD HELPER" -> "Toggle". The state of this toggle will indicate if the task has been performed.
* import blueprint by going to "Configuration" -> "Blueprints" -> "Import Blueprint" -> https://github.com/udorda/HA_DoneChecker/blob/main/DoneChecker.yaml