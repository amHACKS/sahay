# Sahay - सहाय - A Way to Give Back
<img src="/images/sahay_all_compressed.gif" width="80%">

A platform for youngsters to voluntarily help disabled people and senior citizens during tough times.

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


### Firebase by Google ###
- Using Firebase for saving details was very easy and it was awesome. Here's a snippet
 ```
  HashMap<String, Object> hashMap = new HashMap<>();
                                hashMap.put("email",email);

                                firestore.collection("Users").document(currentUserID).set(hashMap).addOnCompleteListener(new OnCompleteListener<Void>() {
                                    @Override
                                    public void onComplete(@NonNull Task<Void> task) {
                                        if (task.isSuccessful())
                                        {
                                            progressDialog.dismiss();
                                            Intent setupIntent = new Intent(LoginActivity.this, SetupActivity.class);
                                            setupIntent.putExtra("email",email);
                                            setupIntent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK | Intent.FLAG_ACTIVITY_CLEAR_TASK);
                                            startActivity(setupIntent);
                                        }
                                        else
                                        {
                                            progressDialog.dismiss();
                                            String err = task.getException().getMessage();
                                            Toast.makeText(LoginActivity.this, err, Toast.LENGTH_SHORT).show();
                                        }
                                    }
                                });
 ```
- We also used Firebase's ML-Kit to verify if the user is uploading a correct image as that ensures safety of the person being helped.

 ```
  private void verifyImage(){


          FirebaseVisionFaceDetectorOptions highAccuracyOpts =
                  new FirebaseVisionFaceDetectorOptions.Builder()
                          .setPerformanceMode(FirebaseVisionFaceDetectorOptions.ACCURATE)
                          .setLandmarkMode(FirebaseVisionFaceDetectorOptions.ALL_LANDMARKS)
                          .setClassificationMode(FirebaseVisionFaceDetectorOptions.ALL_CLASSIFICATIONS)
                          .build();
          ProfileImageView.setDrawingCacheEnabled(true);
          Bitmap bitmap = Bitmap.createBitmap(ProfileImageView.getDrawingCache());
          FirebaseVisionImage image = FirebaseVisionImage.fromBitmap(bitmap);
          ProfileImageView.setDrawingCacheEnabled(false);
          FirebaseVisionFaceDetector detector = FirebaseVision.getInstance()
                  .getVisionFaceDetector(highAccuracyOpts);
          Task<List<FirebaseVisionFace>> result =
                  detector.detectInImage(image)
                          .addOnSuccessListener(
                                  new OnSuccessListener<List<FirebaseVisionFace>>() {
                                      @Override
                                      public void onSuccess(List<FirebaseVisionFace> faces) {
                                          // Task completed successfully
                                          // ...
                                          Log.d("MainActivity","Faces detected:"+ Integer.toString(faces.size()));
                                          if(faces.size()==0){
                                              //Toast.makeText(SetupActivity.this,"Please insert a proper image",Toast.LENGTH_SHORT).show();
                                              new AlertDialog.Builder(SetupActivity.this)
                                                      .setTitle("Face Recognition")
                                                      .setMessage("Please insert a proper image")
                                                      .setPositiveButton("OK", null)
                                                      .show();
                                          }
                                          else if(faces.size()==1){

                                              up_photo.setVisibility(View.INVISIBLE);
                                              uploadImage();

                                          }
                                      }
                                  })
                          .addOnFailureListener(
                                  new OnFailureListener() {
                                      @Override
                                      public void onFailure(@NonNull Exception e) {
                                          // Task failed with an exception
                                          // ...
                                      }
                                  });


      }
 ```



### Facebook API ###

  Facebook API was mainly used for the register part and we saved users into firebase
  ```
  private void handleFacebookAccessToken(AccessToken token) {

        AuthCredential credential = FacebookAuthProvider.getCredential(token.getToken());
        mAuth.signInWithCredential(credential)
                .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
                    @Override
                    public void onComplete(@NonNull Task<AuthResult> task) {
                        if (task.isSuccessful()) {
                            // Sign in success, update UI with the signed-in user's information
                            FirebaseUser user = mAuth.getCurrentUser();
                        } else {
                            // If sign in fails, display a message to the user.

                        }

                        // ...
                    }
                });
    }
 ```


### Screen Shots of our Application :
<img src = "images/sahay_welcome_page_screenshot.jpg" width = 50%><img src = "images/sahay_upload_request_screenshot.jpg" width = 50%>

