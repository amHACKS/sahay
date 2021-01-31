# Sahay - सहाय - A Way to Give Back
A platform for youngsters to voluntarily help disabled people and senior citizens during tough times.
<img src="/images/sahay_all_compressed.gif" width="80%">

## Overview
<img src="images/sahay_flowchart_2.png" width="80%">

Most Senior citizens and physically challenged people are stuck at home due to the pandemic. A large fraction of them are stuck alone at home, making it difficult for them to get by. Our App aims to make their lives easier by providing a means for them to seek help from volunteers for tasks like 
* Buying and delivering essentials and medicines
* Domestic assistance
* An accident or emergency at home, considering the fact that emergency services in our country are super slow to respond.

 
### Steps for Using ###
  Clone the repo
  ```
  git clone 'https://github.com/Mainakdeb/sahay.git'
  ```
  Open Android Studio or download it
  ```
  https://developer.android.com/studio
  ```
  Firebase usage(Make sure these lines are there in app module of build.gradle file)
  ```
  implementation 'com.google.firebase:firebase-ml-vision:24.0.3'
  implementation 'com.google.firebase:firebase-ml-vision-face-model:20.0.1'
  ```
  Facebook SDK(Make sure these lines are there in app module of build.gradle file)
  ```
  implementation 'com.facebook.android:facebook-android-sdk:[5,6)'
  implementation 'com.facebook.android:facebook-share:[5,6)'
  ```
### WorkFlow of our Application :
- A user logs in or registers through the app using email or Facebook
- Next user uploads personal details.
- Here we ensure a proper photo is uploaded using Firebase's ML-Kit
- Next they go to dashboard where they can help someone or seek help
- A help seeker has the option to give details about what he wants
- A helper has the option to help someone based on the location provided by the help-seeker
- Google Maps was used for this purpose

### Resources ###

- [Java For Android](https://developer.android.com/studio/write/java8-support?gclid=Cj0KCQiAx9mABhD0ARIsAEfpavRC2vOE87xYbFaVWQK0B1cUjnWUG5vh8G-YvZm-i3dQjVucjUW5_UUaAhiZEALw_wcB&gclsrc=aw.ds)
- [Facebook API for Login](https://developers.facebook.com/docs/facebook-login/)
- [Firebase](https://firebase.google.com/)


<h3>Firebase by Google</h3>
<ul>
  <li>Firebase by Google is a very useful tool which helped us a lot to handle the backend part as it made things very easy</li>
  <li>Using Firebase's ML-Kit we were able to make sure that a user is uploading a correct face using face-verification technique ensuring safety of the person being helped</li>
 </ul>


<h3>Facebook API</h3>
<ul>
  <li>Facebook API was mainly used for the register part and we saved users into firebase</li>
  <li>In future we plan to give option to share to facebook as that would be very helpful</li>
</ul>

### Screen Shots of our Application :
