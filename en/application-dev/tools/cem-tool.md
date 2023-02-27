# Common Event Manager

The Common Event Manager provides the common event debugging and testing capabilities that enable you to print common event information and publish common events. With this tool, you can send commands (started with **cem**) in the hdc shell to perform various system operations, such as printing all common event subscribers, sent common events, and recipients, as well as publishing common events.

## Commands

### help

* Function

  Prints help information.

* Method

  ```
  cem help
  ```

### publish

* Function

  Publishes a common event.

* Method

  ```
  cem publish [<options>]
  ```

  The table below describes the available options.

  | Name        | Description                                  |
  | ------------ | ------------------------------------------ |
  | -e/--event   | Name of the common event to publish. Mandatory.                    |
  | -s/--sticky  | Indicates that the common event to publish is sticky. Optional. By default, non-sticky events are published.|
  | -o/--ordered | Indicates that the common event to publish is ordered. Optional. By default, non-ordered events are published.  |
  | -c/--code    | Result code of the common event. Optional.                  |
  | -d/--data    | Data carried in the common event. Optional.                |
  | -h/--help    | Help information.                                  |

* Example

  ```bash
  # Publish a common event named testevent.
  cem publish --event "testevent"
  ```
  
  ![cem-publish-event](figures/cem-publish-event.png)
  
  ```bash
  # Publish a sticky, ordered common event named testevent. The result code of the event is 100 and the data carried is this is data.
  cem publish -e "testevent" -s -o -c 100 -d "this is data"
  ```
  
  ![cem-publish-all](figures/cem-publish-all.png)

### dump

* Function

  Displays information about common events.

* Method

  ```
  cem dump [<options>]
  ```

  The table below describes the available options.

  | Name      | Description                                    |
  | ---------- | -------------------------------------------- |
  | -a/--all   | Information about all common events that have been sent since system startup.|
  | -e/--event | Information about a specific event.                  |
  | -h/--help  | Help information.                                    |

* Example

  ```bash
  # Display details of a common event named testevent.
  cem dump -e "testevent"
  ```

  ![cem-dump-e](figures/cem-dump-e.png)