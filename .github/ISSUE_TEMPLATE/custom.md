---
name: Custom issue template
about: Describe this issue template's purpose here.
title: 'Input '
labels: enhancement
assignees: Tanyajackson638

---

// Define the Worker requiring input
public class UploadWork extends Worker {

   public UploadWork(Context appContext, WorkerParameters workerParams) {
       super(appContext, workerParams);
   }

   @NonNull
   @Override
   public Result doWork() {
       String imageUriInput = getInputData().getString("IMAGE_URI");
       if(imageUriInput == null) {
           return Result.failure();
       }

       uploadFile(imageUriInput);
       return Result.success();
   }
   ...
}

// Create a WorkRequest for your Worker and sending it input
WorkRequest myUploadWork =
      new OneTimeWorkRequest.Builder(UploadWork.class)
           .setInputData(
               new Data.Builder()
                   .putString("IMAGE_URI", "http://...")
                   .build()
           )
           .build();
