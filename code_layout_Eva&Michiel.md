# Business Project Advanced

## Code

### Sensor

```
Sensor (extends DistanceSensor from picozero)
    - distance_in_cm
    - distance_to_floor_in_cm
    - length_in_cm
    > measure()
    > calibrate()
    > update()
    > measure_and_update()
```

> measure()
```
distance_in_cm = distance * 100
```
> calibrate()
```
distance_to_floor_in_cm = distance * 100
```
> update()
```
length_in_cm = distance_to_floor_in_cm - distance_in_cm
```
> measure_and_update()

#### LINKS
[https://www.geeksforgeeks.org/extend-class-method-in-python/](https://www.geeksforgeeks.org/extend-class-method-in-python/)

### SensorArray

```
SensorArray
    - sensors[]
    - min_distance
    - min_distance_sensor
    - min_distance_sensor_index
    - max_length
    - left_right_diff
    - front_back_diff
    - average_min_distance
    - average_max_length
    - average_left_right_diff
    - average_front_back_diff
    > measure_all()
    > calibrate_all()
    > update_all(#shots)
    > stabilize(#shots)
```

> measure_all()
```
sensors[i].measure_and_update()
if (sensors[i].distance_in_cm < min_distance)
    min_distance = sensors[i].distance_in_cm
    min_distance_sensor = sensors[i]
    min_distance_sensor_index = i
    max_length = sensors[i].length_in_cm
```
> calibrate_all()
```
sensors[i].calibrate()
left_right_diff = sensors[2].distance_to_floor_in_cm - sensors[4].distance_to_floor_in_cm
front_back_diff = sensors[1].distance_to_floor_in_cm - sensors[5].distance_to_floor_in_cm
```
> update_all(#shots)
```
for (i = 0; i < #shots; i++)
    measure_all()
    total_min_distance += min_distance
    total_max_length += max_length
average_min_distance = total_min_distance / #shots
average_max_length = total_max_length / #shots
```
> stabilize(#shots)
```
for (i = 0; i < #shots; i++)
    calibrate_all()
    total_left_right_diff += left_right_diff
    total_front_back_diff += front_back_diff
average_left_right_diff = total_left_right_diff / #shots
average_front_back_diff = total_front_back_diff / #shots
```

#### LINKS
[https://www.geeksforgeeks.org/how-to-create-a-list-of-object-in-python-class/](https://www.geeksforgeeks.org/how-to-create-a-list-of-object-in-python-class/)

## UART

> measure [sensor_index]
```
sensor_array.sensors[sensor_index].measure()
print(f"distance in cm: {sensor_array.sensors[sensor_index].distance_in_cm}")
```
> measure_all
```
sensor_array.measure_all()
print(f"sensor {i}: {sensor_array.sensors[i].distance_in_cm}")
```
> calibrate_all
```
sensor_array.calibrate_all()
print(f"distance(s) to floor")
print(f"sensor {i}: {sensor_array.sensors[i].distance_to_floor_in_cm}")
print(f"left - right diff: {sensor_array.left_right_diff}")
print(f"front - back diff: {sensor_array.front_back_diff}")
```
> multishot [#shots]
```
sensor_array.update_all(#shots)
print(f"average min distance: {average_min_distance}")
print(f"average max length: {average_max_length}")
```
> stabilize [#shots]
```
sensor_array.stabilize(#shots)
print(f"average left - right diff: {average_left_right_diff}")
print(f"average front - back diff: {average_front_back_diff}")
```

