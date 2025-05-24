<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.ModuleFitness"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true"
            tools:ignore="ExtraText,Instantiatable">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535"
    tools:context=".MainActivity" >

    <TextView
        android:id="@+id/titlePart2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Module"
        android:textColor="#FF0000"
        android:textSize="60sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.583"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.316"
        tools:ignore="HardcodedText,MissingConstraints" />

    <TextView
        android:id="@+id/titlePart1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Fitness"
        android:textColor="#0077FF"
        android:textSize="60sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.429"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.256"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit"
        android:layout_width="191dp"
        android:layout_height="53dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Выйти"
        android:textColor="#FF0000"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.843"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnRegister"
        android:layout_width="191dp"
        android:layout_height="48dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Зарегистрироваться"
        android:textColor="#119EF6"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.635"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnLogin"
        android:layout_width="167dp"
        android:layout_height="48dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Войти"
        android:textColor="#00FF00"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.743"
        tools:ignore="MissingConstraints" />


</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535">

    <TextView
        android:id="@+id/titlePart3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Регистрация"
        android:textColor="#0077FF"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.211"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit2"
        android:layout_width="127dp"
        android:layout_height="54dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Войти"
        android:textColor="#F3835B"
        android:textSize="24sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.531"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.894"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Логин"
        android:textColor="#C1C1C1"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.183"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.397"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart4"
        android:layout_width="63dp"
        android:layout_height="19dp"
        android:text="Пароль"
        android:textColor="#C1C1C1"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.192"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.574"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit"
        android:layout_width="187dp"
        android:layout_height="52dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Уже есть аккаунт?"
        android:textColor="#F3835B"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.023"
        tools:ignore="HardcodedText,MissingConstraints" />

    <EditText
        android:id="@+id/editTextText"
        android:layout_width="271dp"
        android:layout_height="48dp"
        android:ems="10"
        android:importantForAutofill="no"
        android:inputType="text"
        android:minHeight="48dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.478"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.398"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <EditText
        android:id="@+id/editTextTextPassword3"
        android:layout_width="277dp"
        android:layout_height="54dp"
        android:ems="10"
        android:inputType="textPassword"
        android:minHeight="48dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.573"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535">

    <TextView
        android:id="@+id/titlePart3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Авторизация"
        android:textColor="#F3835B"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.211"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit2"
        android:layout_width="127dp"
        android:layout_height="54dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Войти"
        android:textColor="#0077FF"
        android:textSize="24sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.531"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.894"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Логин"
        android:textColor="#C1C1C1"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.183"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.397"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart4"
        android:layout_width="63dp"
        android:layout_height="32dp"
        android:text="Пароль"
        android:textColor="#C1C1C1"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.192"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.574"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit"
        android:layout_width="236dp"
        android:layout_height="48dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Ещё не зарегистрированы?"
        android:textColor="#0077FF"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.023"
        tools:ignore="HardcodedText,MissingConstraints" />

    <EditText
        android:id="@+id/editTextText"
        android:layout_width="271dp"
        android:layout_height="48dp"
        android:ems="10"
        android:importantForAutofill="no"
        android:inputType="text"
        android:minHeight="48dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.478"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.398"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <EditText
        android:id="@+id/editTextTextPassword3"
        android:layout_width="277dp"
        android:layout_height="54dp"
        android:ems="10"
        android:inputType="textPassword"
        android:minHeight="48dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.573"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535">

    <TextView
        android:id="@+id/titlePart2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Module"
        android:textColor="#FF0000"
        android:textSize="60sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.598"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.47"
        tools:ignore="HardcodedText,MissingConstraints" />

    <TextView
        android:id="@+id/titlePart1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Fitness"
        android:textColor="#0077FF"
        android:textSize="60sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.443"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.41"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit"
        android:layout_width="190dp"
        android:layout_height="48dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Выйти из системы?"
        android:textColor="#0077FF"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.023"
        tools:ignore="HardcodedText,MissingConstraints" />

    <Button
        android:id="@+id/btnExit2"
        android:layout_width="127dp"
        android:layout_height="54dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Выйти"
        android:textColor="#FF0000"
        android:textSize="24sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.077"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.94"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Главное меню"
        android:textColor="#F3835B"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.211"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart5"
        android:layout_width="176dp"
        android:layout_height="86dp"
        android:text="Адрес: Петровская ул., 63, Энгельс"
        android:textColor="#6D6D6D"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.093"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.761"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart34"
        android:layout_width="301dp"
        android:layout_height="30dp"
        android:text="Каждое занятие длится 1 час"
        android:textColor="#000000"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.609"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.597"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart6"
        android:layout_width="144dp"
        android:layout_height="58dp"
        android:text="Телефон: +79170282779"
        android:textColor="#6D6D6D"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.94"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.739"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit2"
        android:layout_width="175dp"
        android:layout_height="61dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Продолжить"
        android:textColor="#0077FF"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.924"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.94"
        tools:ignore="DuplicateIds,MissingConstraints" />

</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535">

    <TextView
        android:id="@+id/titlePart21"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="напишите Вашу цель занятия"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.401"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.696"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart20"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Цель:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.202"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.646"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart19"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="выбор пола"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.233"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.406"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart22"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="напишите Ваш вес"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.277"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.565"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart18"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Пол:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.203"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.355"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit3"
        android:layout_width="175dp"
        android:layout_height="61dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Продолжить"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.873"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <Button
        android:id="@+id/btnExit"
        android:layout_width="187dp"
        android:layout_height="52dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Вернуться назад"
        android:textColor="#F3835B"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.023"
        tools:ignore="HardcodedText,MissingConstraints" />

    <TextView
        android:id="@+id/titlePart3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Характеристика"
        android:textColor="#0077FF"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.211"
        tools:ignore="MissingConstraints" />

    <Spinner
        android:id="@+id/spinner2"
        android:layout_width="147dp"
        android:layout_height="48dp"
        android:spinnerMode="dropdown"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.352" />

    <EditText
        android:id="@+id/editTextText"
        android:layout_width="103dp"
        android:layout_height="48dp"
        android:ems="10"
        android:importantForAutofill="no"
        android:inputType="text"
        android:minHeight="48dp"
        android:text="Вес"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.243"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.516"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535">

    <TextView
        android:id="@+id/titlePart17"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="предлагаемое занятие"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.375"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.535"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit3"
        android:layout_width="175dp"
        android:layout_height="61dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Продолжить"
        android:textColor="#0077FF"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.932"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.944"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <Button
        android:id="@+id/btnExit"
        android:layout_width="187dp"
        android:layout_height="52dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Вернуться назад"
        android:textColor="#0077FF"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.023"
        tools:ignore="HardcodedText,MissingConstraints" />

    <TextView
        android:id="@+id/titlePart3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Занятия"
        android:textColor="#F3835B"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.211"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart9"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Цена: "
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.252"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.609"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart12"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Занятие: "
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.277"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.487"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart11"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Стоимость занятия"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.338"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.653"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart7"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Исходя из Вашего веса и цели"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.495"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.318"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart8"
        android:layout_width="311dp"
        android:layout_height="31dp"
        android:text="были подобраны следующие занятия:"
        android:textColor="#0077FF"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.61"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.358"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit3"
        android:layout_width="177dp"
        android:layout_height="70dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Выбрать самостоятельно"
        android:textColor="#FF0000"
        android:textSize="16sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.034"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.957"
        tools:ignore="DuplicateIds,MissingConstraints" />

</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535">

    <TextView
        android:id="@+id/titlePart14"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Напишите удобное для Вас время (полная дата)"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.522"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.679"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart23"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="представленный тренер"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.186"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.549"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart24"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="представленное занятие"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.188"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.419"
        tools:ignore="MissingConstraints" />

    <EditText
        android:id="@+id/editTextText2"
        android:layout_width="103dp"
        android:layout_height="48dp"
        android:ems="10"
        android:importantForAutofill="no"
        android:inputType="text"
        android:minHeight="48dp"
        android:text="д.м.г|xx:xx"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.412"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.638"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <TextView
        android:id="@+id/titlePart15"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Время:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.134"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.636"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit3"
        android:layout_width="175dp"
        android:layout_height="61dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Записаться"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.483"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.901"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <Button
        android:id="@+id/btnExit"
        android:layout_width="187dp"
        android:layout_height="52dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Вернуться назад"
        android:textColor="#F3835B"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.023"
        tools:ignore="HardcodedText,MissingConstraints" />

    <TextView
        android:id="@+id/titlePart3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Запись"
        android:textColor="#0077FF"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.199"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart9"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Тренер:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.136"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart10"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Занятие:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.141"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.373"
        tools:ignore="MissingConstraints" />

</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535">

    <Button
        android:id="@+id/btnExit4"
        android:layout_width="175dp"
        android:layout_height="61dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Записаться"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.483"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.913"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <EditText
        android:id="@+id/editTextText2"
        android:layout_width="103dp"
        android:layout_height="48dp"
        android:ems="10"
        android:importantForAutofill="no"
        android:inputType="text"
        android:minHeight="48dp"
        android:text="д.м.г|xx:xx"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.412"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.691"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <TextView
        android:id="@+id/titlePart14"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Напишите удобное для Вас время (полная дата)"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.522"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.731"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart15"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Время:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.133"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.687"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit"
        android:layout_width="187dp"
        android:layout_height="52dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Вернуться назад"
        android:textColor="#F3835B"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.023"
        tools:ignore="HardcodedText,MissingConstraints" />

    <TextView
        android:id="@+id/titlePart3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Личная запись"
        android:textColor="#0077FF"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.199"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart11"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="выбор тренера"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.179"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.569"
        tools:ignore="MissingConstraints" />

    <Spinner
        android:id="@+id/spinner"
        android:layout_width="147dp"
        android:layout_height="48dp"
        android:spinnerMode="dropdown"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.56"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.521" />

    <TextView
        android:id="@+id/titlePart9"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Тренер:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.157"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.517"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart13"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="выбор занятия"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.179"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.392"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart10"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Занятие:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.163"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.339"
        tools:ignore="MissingConstraints" />

    <Spinner
        android:id="@+id/spinner2"
        android:layout_width="147dp"
        android:layout_height="48dp"
        android:spinnerMode="dropdown"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.606"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.336" />

</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535">

    <TextView
        android:id="@+id/titlePart30"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ваш вес"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.632"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.763"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart29"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ваш пол"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.485"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.668"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart27"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ваши записи"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.051"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.435"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart28"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ваш логин"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.271"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.569"
        tools:ignore="MissingConstraints" />

    <Spinner
        android:id="@+id/spinner3"
        android:layout_width="147dp"
        android:layout_height="48dp"
        android:spinnerMode="dropdown"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.598"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.371" />

    <Button
        android:id="@+id/btnExit5"
        android:layout_width="234dp"
        android:layout_height="62dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Записаться снова"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.934"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <Button
        android:id="@+id/btnExit"
        android:layout_width="187dp"
        android:layout_height="52dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Выйти из системы"
        android:textColor="#0077FF"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.023"
        tools:ignore="HardcodedText,MissingConstraints" />

    <TextView
        android:id="@+id/titlePart3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Личный кабинет"
        android:textColor="#F3835B"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.496"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.25"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart26"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Записи:"
        android:textColor="#0077FF"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.055"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.371"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart16"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Пол"
        android:textColor="#F3835B"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.452"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.62"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart12"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Логин"
        android:textColor="#F3835B"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.278"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.516"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart25"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Вес"
        android:textColor="#F3835B"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.58"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.723"
        tools:ignore="MissingConstraints" />

</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535">

    <TextView
        android:id="@+id/titlePart33"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="стоимость упражнения"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.209"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.721"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart10"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Занятие:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.18"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.311"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart11"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="выбранный тренер"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.2"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.492"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart9"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Тренер:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.175"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.438"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart14"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="выбранное время"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.179"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.599"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart15"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Время:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.148"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.561"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart32"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Цена:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.145"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.68"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart13"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="выбранное занятие"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.226"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.363"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExit4"
        android:layout_width="224dp"
        android:layout_height="59dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Закрыть форму"
        android:textColor="#0077FF"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.918"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <Button
        android:id="@+id/btnExit6"
        android:layout_width="143dp"
        android:layout_height="58dp"
        android:layout_marginHorizontal="8dp"
        android:backgroundTint="#000000"
        android:text="Отменить"
        android:textColor="#FF0000"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.059"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        android:layout_marginTop="64dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.916"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <TextView
        android:id="@+id/titlePart3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Форма записи"
        android:textColor="#0077FF"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.362"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.155"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePart31"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="№1"
        android:textColor="#0077FF"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.882"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.155"
        tools:ignore="MissingConstraints" />

</androidx.constraintlayout.widget.ConstraintLayout>
