# Zoomy
Zoomy is an easy to use pinch-to-zoom Android library

![alt tag](art/zoomy.gif)
## Installation

Zoomy is available in the JCenter, so you just need to add it as a dependency
```gradle
compile 'com.ablanco.zoomy:zoomy:{latest version}'
```
where `{latest version}` corresponds to published version in JCenter [ ![Download](https://api.bintray.com/packages/ablanco/maven/zoomy/images/download.svg) ](https://bintray.com/ablanco/maven/zoomy/_latestVersion)

##Usage 

To start using Zoomy, just register the View you want to be zoomable

```java

Zoomy.Builder builder = new Zoomy.Builder(this).target(mZoomableView);
builder.register();
            
```

Thats all. Now your views can be pinch-zoomed!

##Customization

Zoomy allows a few customizations in its behavior:

+ Use ZoomyConfig to change default configuration flags

```java
ZoomyConfig config = new ZoomyConfig();
config.setZoomAnimationEnabled(false); //Enables zoom out animation when view is released (true by default)
config.setImmersiveModeEnabled(false); //Enables entering in inmersive mode when zooming a view (true by default)          
```

+ Now set this as the default configuration across all Zoomy registered views
```java
Zoomy.setDefaultConfig(config);           
```

Zoomy builder also allows some customization

+ Zoomy config flags can also be set when building Zoomy registration. 
This flags will always override default ZoomyConfig flags.
```java
    Zoomy.Builder builder = new Zoomy.Builder(this)
                    .target(mZoomableView)
                    .enableImmersiveMode(false)
                    .animateZooming(false);
```

+ You can add callbacks to listen for specific events. Because Zoomy works by attaching a View.OnTouchListener to the registered View,
View.OnClickListener can`t be set along with Zoomy, so a TapListener is provided to ensure the View still can listen for click events.
A ZoomListener is also provided if you are interested in zoom events.
```java
 Zoomy.Builder builder = new Zoomy.Builder(this)
                    .target(mZoomableView)
                    .tapListener(new TapListener() {
                        @Override
                        public void onTap(View v) {
                            //View tapped, do stuff
                        }
                    })
                    .zoomListener(new ZoomListener() {
                        @Override
                        public void onViewStartedZooming(View view) {
                            //View started zooming
                        }

                        @Override
                        public void onViewEndedZooming(View view) {
                            //View ended zooming
                        }
                    });        
```

+ It is possible to change the interpolator used when animating ending zoom event.

```java
   Zoomy.Builder builder = new Zoomy.Builder(this)
                    .target(mZoomableView)
                    .interpolator(new OvershootInterpolator());
```

License
=======

    Copyright 2017 Álvaro Blanco Cabrero
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
