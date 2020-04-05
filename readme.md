# Micro animations with lottie

![lottie:3.4.0](https://img.shields.io/badge/lottie-3.4.0-green)
![bodymovin:5.6.5](https://img.shields.io/badge/bodymovin-5.6.5-blue)
![issues:3 open](https://img.shields.io/badge/issues-3%20open-black)

## demo

menu icon animation                                 | search icon animation
:--------------------------------------------------:|:------------------------------------------------------:
<img src="gifs/menu-close-menu-60frames.gif" width="200">|<img src="gifs/search-close-search-60frames.gif" width="200">

## setup and installation

### For Android

to implement the animations into your code, first start by adding lottie in your dependancies like this;

```
dependencies {
...
 //Lottie Library
implementation ‘com.airbnb.android:lottie:$lottieVersion’
...
} 
```
at the time of making this mini project the lottie version is 3.4.0

*you can read more here: https://github.com/airbnb/lottie-android and scroll to the bottom*

now sync your gradle files.

the code below will make the animation **NOT** auto-play

``` <com.airbnb.lottie.LottieAnimationView
 android:id=”@+id/lav_myanim” <!-- give the animation id -->
 app:lottie_autoPlay=”false” <!-- stating that it should NOT autoplay -->
 app:lottie_fileName=”{name-of-json}.json <!-- this is the name of the animation.json you want, without the curly braces -->
 app:lottie_loop=”false” /> 
 ```

 in your java class import lottie animation view

 ```
 import com.airbnb.lottie.LottieAnimationView; 
 ```

then declare your variable

``` lottieAnimationView myanim; 
```
then define your function and call the play animation methods

```	int action=0;
	myanim = findViewById(R.id.lav_myanim);
        myanim.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                changeState();
            }
        }); 
```
 and this is the changeState function

  ```    
  private void changeState() {
        if (action == 0) {
        //the animation from start to half, which is the completion of the second state. i.e the arrival of the animation at the close button
        //Here, calculation is done on the basis of start and stop frame divided by the total number of frames
        //for the menu-close animation frames are 60
        //for the search-close animation frames are 98

            myanim.setMinAndMaxProgress(0f, 0.43f); 
           
            myyanim.playAnimation();
            action = 1;

            //do something
        } 

		//from the close state to the original state of the animation
        else {
            myanim.setMinAndMaxProgress(0.5f, 1f);
            myanim.playAnimation();
            action = 0;

            //do something
        }
    }
```
### For Web

With basic vanilla Javascript.
First start by downloading lottie.js. You can do so directly via this link  https://www.dropbox.com/s/fvl9s396m4vmcpk/lottie.js?dl=0 
or
you can go to the lottie web github page and get the lottie.js file from the build/player/ folder for the latest build.
Here's the link https://github.com/airbnb/lottie-web.

secondly, Include the scripton your website

``` <script src='../assets/js/plugins/lottie.js'></script> <!--  the location of your lottie.js in your project--> ```

next, create a div and give your div an id

``` <div onclick="animate();" id="lot_myanim"></div> ```

now add the following script
```function animate(){
	var animData = {
	        wrapper: document.getElementById('lot_myanim'),
	        animType: 'html',
	        loop: false,
	        prerender: false,
	        autoplay: false,
	        path: 'name-of-anim.json'
	    };

	var anim = bodymovin.loadAnimation(animData);
	anim.play();
	}
}
```

*documentation: https://airbnb.io/lottie/#/web*

### React Native

first start by importing the lottie web package with 

```	npm install --save lottie-web ```

then import the lottie module and the animation.json file

```import lottie from 'lottie-web';
import animationData from '../plugins/lottie/name-of-animation.json';
```

call the loadAnimation to start the animation
```
    animObj = lottie.loadAnimation({
      container: this.animBox, // the dom element that will contain the animation
      renderer: 'svg',
      loop: false,
      autoplay: false,
      animationData: animationData // the path to the animation json
    });
```
then

```
myAnimStop(){
    animObj.stop();
  }
myAnimPlay() {
animObj.play();
}
  render() {
    return (
      <div className="App">
        <h2>This is my Lottie Web animation</h2>
        {/* This is you wrapper where animation will load */}
        <div  onClick={this.myAnimPlay} style={{width: 400, margin: '0 auto'}} ref={ ref => this.animBox = ref}></div>
        <button onClick={this.myAnimStop}>Stop</button>
      </div>
    );
  }
```
## contribution

You can contribute to this project by reaching me via dm or shooting me an [email](mailto:leonkipkoech00@gmail.com).<br>
Here's the [contribution](contribution.md) guide.
  
## license

This project is under the [mit license](https://github.com/leonkoech/Micro-Animations/license.md).

## challanges

This was a fast mini-project I did when I took a break from some online classes. So there are installation guides that I have not included.
Also, some of the ones I've included lack the stop when animation is halfway in terms of frame count. and continue to the end when clicked again.

- [x] java/android onclick stop animation and continue when clicked again
- [x] react native onclick start animation
- [x] react native button to stop animation
- [x] vanilla javascript onclick start animation
- [ ] react native onclick stop animation and continue when clicked again
- [ ] vanilla javascript onclick stop animation and continue when clicked again
- [ ] ios/mac on click to start or stop animation
