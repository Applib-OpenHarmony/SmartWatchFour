## Library Name:
Smart Watch 4

## Library Version:
1.0.0
## Library Release Date:
26-05-2022
## Library Overview:
Smart Watch four shows following functionalites;
- It fetches weather details based on the location of the user.
- Shows current date and time
- Calculates Number of steps walked ,bpm andCalories burned 
- Displays Remainder.
<hr>

### GitHub link: [Smart Watch four](https://github.com/applibgroup/smart_watch_four)
<hr>

## Screenshot of the Library:
![image](https://user-images.githubusercontent.com/77436328/173221960-3695d35a-ce63-44c4-b8f6-add8a406c65d.png)




# Library Feature1:
### Description:
It fetches weather details based on the location of the user.
### Code Snippet:
```
    fecthWeather: function () {
        let locData;
        geolocation.getLocation({
            success: function (data) {
                locData = data;
                console.log("The location fetched:" + JSON.stringify(data));
            },
            fail: function (data, code) {
                console.log('fail to get location. code:' + code + ', data:' + data);
            },
            complete: function () {
                console.log('in Complete');
            }
        })
        console.log('Location Data: ' + JSON.stringify(locData) + " lat: " + locData.latitude + " long: " + locData.longitude);

        this.lat = locData.latitude;
        this.long = locData.longitude;

        console.log("Lat : " + this.lat + " Long : " + this.long);

        let data;
        fetch.fetch({
            url: 'https://api.openweathermap.org/data/2.5/weather?lat=' + this.lat + '&lon=' + this.long + '&appid=9ca3abfc02f621a4fe7696f670f04a57',
            responseType: "JSON",
            method: 'GET',
            success: function (resp) {
                data = JSON.parse(resp.data);
                console.log("Data :" + data + " " + resp + " ");
            },
            fail: (data, code) => {
                console.log("fail data: " + JSON.stringify(data) + " fail code: " + code);
            },
            complete: () => {
                this.weather = data.weather[0].main;
                console.log("Weather :" + this.weather + " " + this.weather[0].main);
            }
        })
    }
```

### Screenshot:
![image](https://user-images.githubusercontent.com/77436328/173222104-56e161e8-447c-4ad2-b3a0-8561fe759fc2.png)

`Note:` Since latitude: `121.61934` and longitude: `31.257907` does not exists it throwing an error.

### Flow chart description:
In fecthWeather function it will first fetches the locations details of the user i.e latitude and longitude,
 using openweather api fetches the weather details based on the latitude and longitude.



# Library Feature2:
### Description:
Fetches BPM, Calories burned and notification using an [API](https://mocki.io/v1/cb0cd987-0c49-4e7c-9475-fb533723e2fd) created by me.
### Code Snippet:
```
    fecthData: function () {
        let data;
        fetch.fetch({
            url: 'https://mocki.io/v1/cb0cd987-0c49-4e7c-9475-fb533723e2fd',
            responseType: "json",
            method: 'GET',

            success: function (res) {
                data = JSON.parse(res.data);
                console.log("Data :" + data + " " + JSON.stringify(res) + " ");
            },

            fail: (data, code) => {
                console.log("Fail Data: noti " + JSON.stringify(data) + " fail code: " + code);
            },
            complete: () => {
                this.bpm = data.bpm;
                this.kcal = data.cal;
                this.noti = data.noti;
                console.log(this.bpm + " " + this.kcal + " " + this.noti);
            }
        })
    }
```
<!--img src="https://user-images.githubusercontent.com/77436328/173222109-a817734a-5dae-48d0-b7b6-809b6dc162d9.png" width="800" height="500"-->
### Screenshot: 
![image](https://user-images.githubusercontent.com/77436328/173222119-83ca8fa8-c3d4-42c1-8f04-e4722420a9f7.png)

# Library Feature3:
### Description: 
Calculates number of steps walked.

### Code Snippet:
```
function subscribePedometerSensor(context) {
    sensor.subscribeStepCounter({
        success: function (ret) {
            context.step = ret.steps.toString()
        },
        fail: function (data, code) {
            console.log('Subscription failed. Code: ' + code + '; Data: ' + data)
        }
    })
}

function verifyPermissions() {
    var context = ability_featureAbility.getContext()
    let permission = "ohos.permission.ACTIVITY_MOTION"
    var result = new Promise((resolve, reject) => {
        context.verifyPermission(permission)
            .then((data) => {
                resolve(true)
            }).catch((error) => {
            reject(false)
        })
    })
    return result
}
```
### Screenshot:
<img src="https://user-images.githubusercontent.com/77436328/173222128-01fc70ca-a3f3-4cb6-8505-6eacae6ecd7b.png" width="200" height="100">



## Advanced feature that could be implemented in Future in this library: 
Calculating Blood Pressure and Calories Burned using respective API’s.
## Conclusion:
smart watch four calculates Number of steps walked, BPM, Calories burned, fetches date and time and weather details based on location and notifications.

