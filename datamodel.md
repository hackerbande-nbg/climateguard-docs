# sensormetrics
- timestamp_device
- timestamp_server
- temperature
- humidity
- device_id

# hardware_revisions
- hardware_id
- version_name
- specification_repo
- specification_commit
- specification_file_path

# software_versions
- software_id
- version_name
- git_commit

# devices

- device_id
- name
- hardware_id
- software_id
- latitude
- longitude
- created_at
- appeui
- deveui
- appkey
- ground_cover(enum))
  - in 10 meter around the sensor
  - allowed values:
    - earth
    - grass
    - concrete
    - asphalt
    - cobblestone
    - water
    - sand
    - other
- height_above_ground(int)
- shading(enum)
  - allowed values:
    - 1
    - 2
    - 3
    - 4
    - 5
- close_to_a_tree(boolean)
  - if a tree is <3m away
- close_to_water(boolean)
  - significant water body is <200m
- orientation(enum)
  - which side is the sensor facing
  - allowed values:
    - north
    - east
    - west
    - south
- distance_to_next_building_cm(int)
- 
