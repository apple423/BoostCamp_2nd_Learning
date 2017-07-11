# 안드로이드 2주차 커리큘럼
안드로이드 개발시 필요한 토스트나 스낵바 그리고 인텐트 등을 살펴보고 화면 구성시 자주 사용하는 툴바와 프래그먼트에 대해서 살펴본다. 또한 안드로이드에서 사용할 수 있는 데이터 저장소의 종류를 살펴보고 이를 활용하기 위한 코드를 이해한다.

## 1. 알림 기능 살펴보기
* 토스트 : 적은 양의 메시지를 빠르게 보여주는데 좋은 뷰

  - 이미지 : ![toastImage](toastImage.png)

  - 상속계층도

		    java.lang.Object
		      ↳android.widget.Toast

  - 주요 특징
	 - static Toast makeText(Context context, CharSequence text, int duration)
	  : 텍스트 뷰를 포함한 토스트를 만든다.

	 - show()
	  : 특정 duration동안 토스트를 보여준다.


* 스낵바 : 동작에 따른 짧은 메세지를 보여주기 위한 기능

  - 이미지 : ![snackBar](snackBar.png)

  - 상속계층도

        java.lang.Object
        ↳	android.support.design.widget.BaseTransientBottomBar
           <android.support.design.widget.Snackbar>
        ↳	android.support.design.widget.Snackbar

  - 주요 특징
    - static Snackbar make(View view, CharSequence text, int duration)
    : 스낵바를 만드는 메소드.

    - Snackbar setAction(CharSequence text, View.OnClickListener listener)
    : 스낵바에 Action을 설정한다. 리스너는 null가능
      리스너가 null일시 Action은 보이지 않는다.

* 대화상자 : 대화상자는 사용자에게 결정을 내리거나 추가 정보를 입력하라는 작은 창

  - 이미지 : ![dialogs](dialogs.png)

  - 상속계층도

          java.lang.Object
           ↳	android.app.Dialog

          Known Direct Subclasses
          AlertDialog,AppCompatDialog,CharacterPickerDialog,Presentation

          Known Indirect Subclasses
          AlertDialog,BottomSheetDialog,DatePickerDialog,MediaRouteChooserDialog,
          MediaRouteControllerDialog,ProgressDialog,TimePickerDialog


  - 대화상자 생성
    - DialogFragment를 상속 받고 onCreateDialog를 오버라이드

  ```{.java id:"chj4zb1ij9"}
      public class FireMissilesDialogFragment extends DialogFragment {
      @Override
      public Dialog onCreateDialog(Bundle savedInstanceState) {
          // Use the Builder class for convenient dialog construction
          AlertDialog.Builder builder = new AlertDialog.Builder(getActivity());
          builder.setMessage(R.string.dialog_fire_missiles)
                 .setPositiveButton(R.string.fire, new DialogInterface.OnClickListener() {
                     public void onClick(DialogInterface dialog, int id) {
                         // FIRE ZE MISSILES!
                     }
                 })
                 .setNegativeButton(R.string.cancel, new DialogInterface.OnClickListener() {
                     public void onClick(DialogInterface dialog, int id) {
                         // User cancelled the dialog
                     }
                 });
          // Create the AlertDialog object and return it
          return builder.create();
      }
  }
  ```

  - 대화상자 종류 :
  Basic Dialog : 가장 기초적인 방법의 DialogFragment 사용한 대화상자
  AlterDialog : 경고를 보여주기 위한 대화상자
  DatePickerDialog 또는 TimePickerDialog : 미리 정의된 UI를 통해 시간이나 날짜를 선택 할 수 있도록 하는 대화상자


* 통지(Notification) : 애플리케이션의 정상 UI 외부에서 사용자에게 표시할 수 있는 메시지

  - 이미지 : ![notification](notification.png)

  - 상속계층도

          java.lang.Object
           ↳ android.app.Notification

  - 필수 통지 콘텐츠
  Notification 객체는 다음을 반드시 포함해야 합니다.
    - setSmallIcon()이 설정한 작은 아이콘
    - setContentTitle()이 설정한 제목
    - setContentText()이 설정한 세부 텍스트

  - 통지 생성
   NotificationCompat.Builder 개체에서 알림에 대한 UI 정보와 작업을 지정합니다.
   알림 자체를 생성하려면 NotificationCompat.Builder.build()를 호출합니다.
   이는 사양이 포함된 Notification 객체를 반환합니다.
   알림을 발행하려면 NotificationManager.notify()를 호출해서 시스템에 Notification 객체를 전달합니다

  - 예제
  ```{.java}
        NotificationCompat.Builder mBuilder =
            new NotificationCompat.Builder(this)
            .setSmallIcon(R.drawable.notification_icon)
            .setContentTitle("My notification")
            .setContentText("Hello World!");
    // Creates an explicit intent for an Activity in your app
    Intent resultIntent = new Intent(this, ResultActivity.class);

    // The stack builder object will contain an artificial back stack for the
    // started Activity.
    // This ensures that navigating backward from the Activity leads out of
    // your application to the Home screen.
    TaskStackBuilder stackBuilder = TaskStackBuilder.create(this);
    // Adds the back stack for the Intent (but not the Intent itself)
    stackBuilder.addParentStack(ResultActivity.class);
    // Adds the Intent that starts the Activity to the top of the stack
    stackBuilder.addNextIntent(resultIntent);
    PendingIntent resultPendingIntent =
            stackBuilder.getPendingIntent(
                0,
                PendingIntent.FLAG_UPDATE_CURRENT
            );
    mBuilder.setContentIntent(resultPendingIntent);
    NotificationManager mNotificationManager =
        (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
    // mId allows you to update the notification later on.
    mNotificationManager.notify(mId, mBuilder.build());

  ```


## 2. 인텐트와 액티비티 실행 살펴보기
* 인텐트의 이해
* 인텐트 활용 예시
* 서로 다른 액티비티 실행 방법

## 3. 툴바와 프래그먼트 그리고 머티리얼디자인 살펴보기
* 툴바의 이해
* 프래그먼트의 이해
* 프래그먼트를 활용한 화면 구성
* CoordinatorLayout, CollapsingToolbarLayout
* 머티리얼 디자인의 이해

## 4. 안드로이드스튜디오 템플릿을 활용한 프로젝트 생성하기
* 네비게이션 드로어 프로젝트 생성 및 코드 분석
* 하단 네비게이션 프로젝트 생성 및 코드 분석
* 구글 맵 프로젝트 생성 및 코드 분석

## 5. 안드로이드 저장소 살펴보기
* 프리퍼런스(Preference) 활용
* 파일 활용
* 데이터베이스(SQLite) 활용- 토스트
