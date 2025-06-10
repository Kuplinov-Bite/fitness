package com.example.modulefitness;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class ScreenActivity1 extends AppCompatActivity {

    Button btnReg;
    Button btnAuth;
    Button btnExit;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.screen1);

        btnReg = findViewById(R.id.btnRegister);
        btnReg.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity1.this, ScreenActivity2.class);
                startActivity(intent);
            }
        });

        btnAuth = findViewById(R.id.btnAuth);
        btnAuth.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity1.this, ScreenActivity3.class);
                startActivity(intent);
            }
        });

        btnExit = findViewById(R.id.btnExit);
        btnExit.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finishAffinity();
                System.exit(0);
            }
        });

        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
    }
}

package com.example.modulefitness;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.util.Log;
import android.util.Pair;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import org.json.JSONObject;

import java.io.IOException;

import okhttp3.MediaType;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;

public class ScreenActivity2 extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Button btnHaveAcc;
        Button btnEnter;

        EditText fieldLogin;
        EditText fieldPassword;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.screen2);

        btnHaveAcc = findViewById(R.id.btnHaveAcc);
        btnHaveAcc.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity2.this, ScreenActivity3.class);
                startActivity(intent);
            }
        });

        String supabaseUrl = "https://mhsfkzimnqkhwjrkeuuw.supabase.co";
        String supabaseKey = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im1oc2ZremltbnFraHdqcmtldXV3Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NDkyMzk0MjksImV4cCI6MjA2NDgxNTQyOX0.z5UYbbBiT7AfnMoYcwAVEIg1zmy4YRRYO_1w96DST3o";
        OkHttpClient client = new OkHttpClient();
        MediaType JSON = MediaType.get("application/json; charset=utf-8");

        btnEnter = findViewById(R.id.btnEnter);
        fieldLogin = findViewById(R.id.fieldLogin);
        fieldPassword = findViewById(R.id.fieldPassword);
        btnEnter.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String login = fieldLogin.getText().toString().trim();
                String password = fieldPassword.getText().toString().trim();

                if (login.length() > 3 && password.length() > 3) {
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_enter", login);
                    editor.apply();

                    JSONObject json = new JSONObject();
                    try {
                        json.put("login", login);
                        json.put("password", password);
                    } catch (Exception e) {
                        e.printStackTrace();
                    }

                    RequestBody body = RequestBody.create(json.toString(), JSON);

                    Request request = new Request.Builder()
                            .url(supabaseUrl + "/auth/v1/signup")
                            .addHeader("apikey", supabaseKey)
                            .addHeader("Content-Type", "application/json")
                            .post(body)
                            .build();
                    new Thread(() -> {
                        try {
                            Response response = client.newCall(request).execute();
                            if (response.isSuccessful()) {
                                runOnUiThread(() -> Toast.makeText(ScreenActivity2.this, "Регистрация успешна", Toast.LENGTH_SHORT).show());
                                Log.d("Supabase", "Ответ: " + response.body().string());
                            } else {
                                runOnUiThread(() -> Toast.makeText(ScreenActivity2.this, "Ошибка: " + response.code(), Toast.LENGTH_SHORT).show());
                                Log.e("Supabase", "Ошибка: " + response.body().string());
                            }
                        } catch (IOException e) {
                            runOnUiThread(() -> Toast.makeText(ScreenActivity2.this, "Ошибка сети", Toast.LENGTH_SHORT).show());
                            Log.e("Supabase", "IOException: " + e.getMessage());
                        }
                    }).start();
                } else {
                    Toast.makeText(ScreenActivity2.this, "Введён короткий логин или пароль", Toast.LENGTH_SHORT).show();
                }


                Intent intent = new Intent(ScreenActivity2.this, ScreenActivity4.class);
                startActivity(intent);
            }
        });
    }
}

package com.example.modulefitness;

import android.annotation.SuppressLint;
import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

public class ScreenActivity3 extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Button btnGetAcc;
        Button btnEnter;

        EditText fieldLogin2;
        EditText fieldPassword2;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.screen3);

        btnGetAcc = findViewById(R.id.btnGetAcc);
        btnGetAcc.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity3.this, ScreenActivity2.class);
                startActivity(intent);
            }
        });
        btnEnter = findViewById(R.id.btnEnter2);
        fieldLogin2 = findViewById(R.id.fieldLogin2);
        fieldPassword2 = findViewById(R.id.fieldPassword2);
        btnEnter.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String login = fieldLogin2.getText().toString().trim();
                String password = fieldPassword2.getText().toString().trim();

                if (login.length() > 3 && password.length() > 3)
                {
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_enter", login);
                    editor.apply();

                    Intent intent = new Intent(ScreenActivity3.this, ScreenActivity9.class);
                    startActivity(intent);
                }else {
                    Toast.makeText(ScreenActivity3.this, "Введён короткий логин или пароль", Toast.LENGTH_SHORT).show();
                }
            }
        });
    }
}

package com.example.modulefitness;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.appcompat.app.AppCompatActivity;

public class ScreenActivity4 extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Button btnExitAcc;
        Button btnContinue;
        Button btnExit2;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.screen4);

        btnExitAcc = findViewById(R.id.btnExitAcc);
        btnExitAcc.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity4.this, ScreenActivity1.class);
                startActivity(intent);
            }
        });

        btnContinue = findViewById(R.id.btnContinue);
        btnContinue.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity4.this, ScreenActivity5.class);
                startActivity(intent);
            }
        });

        btnExit2 = findViewById(R.id.btnExit2);
        btnExit2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finishAffinity();
                System.exit(0);
            }
        });
    }
}

package com.example.modulefitness;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.text.InputFilter;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Spinner;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class ScreenActivity5 extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Button btnBack;
        Button btnContinue2;

        Spinner listGender;
        EditText fieldWeight;
        EditText fieldAge;
        EditText fieldPurpose;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.screen5);

        btnBack = findViewById(R.id.btnBack);
        btnBack.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity5.this, ScreenActivity4.class);
                startActivity(intent);
            }
        });

        fieldPurpose = findViewById(R.id.fieldPurpose);
        fieldPurpose.setFilters(new InputFilter[] {
                (source, start, end, dest, dstart, dend) -> {
                    for (int i = start; i < end; i++) {
                        char c = source.charAt(i);
                        if (!Character.toString(c).matches("[а-яА-ЯёЁ]")) {
                            return "";
                        }
                    }
                    return null; //
                }
        });

        listGender = findViewById(R.id.listGender);
        String[] gender = {"Мужской", "Женский"};

        ArrayAdapter<String> adapter = new ArrayAdapter<>(
                this,
                android.R.layout.simple_spinner_item,
                gender
        );
        adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        listGender.setAdapter(adapter);

        listGender.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                String selectedItem = gender[position];
                if (position != 0) {
                    Toast.makeText(ScreenActivity5.this, "Вы выбрали пол: " + selectedItem, Toast.LENGTH_SHORT).show();
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_selected", selectedItem);
                    editor.apply();
                }
            }
            @Override
            public void onNothingSelected(AdapterView<?> parent) {
                // ничего
            }
        });

        btnContinue2 = findViewById(R.id.btnContinue2);
        fieldWeight = findViewById(R.id.fieldWeight);
        fieldAge = findViewById(R.id.fieldAge);
        ArrayList<String> listPurpose = new ArrayList<>(Arrays.asList("похудение", "масса", "энергия", "покой"));
        btnContinue2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String purposeString = fieldPurpose.getText().toString().trim();
                String ageIf = fieldAge.getText().toString().trim();
                int ageAccess = Integer.parseInt(ageIf);

                if (purposeString == "похудение" && ageAccess < 40)
                {
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_task", purposeString);
                    editor.apply();

                    SharedPreferences prefs2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor2 = prefs2.edit();
                    editor.putString("price1", purposeString);
                    editor.apply();
                } if (purposeString == "похудение" && ageAccess > 40) {
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_task_old", purposeString);
                    editor.apply();

                    SharedPreferences prefs2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor2 = prefs2.edit();
                    editor.putString("price2", purposeString);
                    editor.apply();
                }if (purposeString == "масса" && ageAccess < 40) {
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_task2", purposeString);
                    editor.apply();

                    SharedPreferences prefs2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor2 = prefs2.edit();
                    editor.putString("price3", purposeString);
                    editor.apply();
                }if (purposeString == "масса" && ageAccess > 40) {
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_task_old2", purposeString);
                    editor.apply();

                    SharedPreferences prefs2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor2 = prefs2.edit();
                    editor.putString("price4", purposeString);
                    editor.apply();
                }if (purposeString == "энергия" && ageAccess < 40) {
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_task3", purposeString);
                    editor.apply();

                    SharedPreferences prefs2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor2 = prefs2.edit();
                    editor.putString("price5", purposeString);
                    editor.apply();
                }if (purposeString == "энергия" && ageAccess > 40) {
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_task_old3", purposeString);
                    editor.apply();

                    SharedPreferences prefs2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor2 = prefs2.edit();
                    editor.putString("price6", purposeString);
                    editor.apply();
                }if (purposeString == "покой" && ageAccess < 40) {
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_task4", purposeString);
                    editor.apply();

                    SharedPreferences prefs2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor2 = prefs2.edit();
                    editor.putString("price7", purposeString);
                    editor.apply();
                }if (purposeString == "покой" && ageAccess > 40) {
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_task_old4", purposeString);
                    editor.apply();

                    SharedPreferences prefs2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor2 = prefs2.edit();
                    editor.putString("price8", purposeString);
                    editor.apply();
                }

                if (fieldWeight.length() > 1 && fieldAge.length() > 1 && fieldPurpose.length() > 4 && listPurpose.contains(purposeString))
                {
                    String weight = fieldWeight.getText().toString().trim();
                    String age = fieldAge.getText().toString().trim();
                    String purp = fieldPurpose.getText().toString().trim();
                    SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor = prefs.edit();
                    editor.putString("user_weight", weight);
                    editor.apply();

                    SharedPreferences prefs2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor2 = prefs2.edit();
                    editor.putString("user_age", age);
                    editor.apply();

                    SharedPreferences prefs3 = getSharedPreferences("myPrefs", MODE_PRIVATE);
                    SharedPreferences.Editor editor3 = prefs3.edit();
                    editor.putString("user_purpose", purp);
                    editor.apply();

                    Intent intent = new Intent(ScreenActivity5.this, ScreenActivity6.class);
                    startActivity(intent);
                }else
                {
                    Toast.makeText(ScreenActivity5.this, "Выберите пол, вес, цель и возраст ", Toast.LENGTH_SHORT).show();
                }
            }
        });
    }
}

package com.example.modulefitness;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

import org.w3c.dom.Text;

import java.util.ArrayList;
import java.util.Arrays;

public class ScreenActivity6 extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Button btnBack2;
        Button btnChooseSelf;
        Button btnContinue3;

        TextView titleTask;
        TextView titleTaskOld;
        TextView titleTask2;
        TextView titleTaskOld2;
        TextView titleTask3;
        TextView titleTaskOld3;
        TextView titleTask4;
        TextView titleTaskOld4;

        TextView titlePrice1;
        TextView titlePriceOld;
        TextView titlePrice2;
        TextView titlePriceOld2;
        TextView titlePrice3;
        TextView titlePriceOld3;
        TextView titlePrice4;
        TextView titlePriceOld4;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.screen6);

        titleTask = findViewById(R.id.titleTask);
        SharedPreferences prefsTask = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userPurpose = prefsTask.getString("user_task", "Нет занятия");

        titlePrice1 = findViewById(R.id.titlePrice);
        SharedPreferences prefsPrice1 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String priceText1 = prefsPrice1.getString("price1", "Нет цены");

        titleTask.setText("Занятие: Табата");
        titlePrice1.setText("Цена: 799 рублей");

        titleTaskOld = findViewById(R.id.titleTask);
        SharedPreferences prefsTaskOld = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userPurposeOld = prefsTask.getString("user_task_old", "Нет занятия");

        titlePriceOld = findViewById(R.id.titlePrice);
        SharedPreferences prefsPriceOld = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String priceTextOld = prefsPriceOld.getString("price2", "Нет цены");

        titleTaskOld.setText("Занятие: Йога");
        titlePriceOld.setText("Цена: 599 рублей");

        titleTask2 = findViewById(R.id.titleTask);
        SharedPreferences prefsTask2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userPurpose2 = prefsTask2.getString("user_task2", "Нет занятия");

        titlePrice2 = findViewById(R.id.titlePrice);
        SharedPreferences prefsPrice2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String priceText2 = prefsPrice2.getString("price3", "Нет цены");

        titleTask2.setText("Занятие: Силовой тренинг");
        titlePrice2.setText("Цена: 899 рублей");

        titleTaskOld2 = findViewById(R.id.titleTask);
        SharedPreferences prefsTaskOld2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userPurposeOld2 = prefsTaskOld2.getString("user_task_old2", "Нет занятия");

        titlePriceOld2 = findViewById(R.id.titlePrice);
        SharedPreferences prefsPriceOld2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String priceTextOld2 = prefsPriceOld2.getString("price4", "Нет цены");

        titleTaskOld2.setText("Занятие: Пилатес");
        titlePriceOld2.setText("Цена: 699 рублей");

        titleTask3 = findViewById(R.id.titleTask);
        SharedPreferences prefsTask3 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userPurpose3 = prefsTask3.getString("user_task3", "Нет занятия");

        titlePrice3 = findViewById(R.id.titlePrice);
        SharedPreferences prefsPrice3 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String priceText3 = prefsPrice3.getString("price5", "Нет цены");

        titleTask3.setText("Занятие: Кардио-танцы");
        titlePrice3.setText("Цена: 399 рублей");

        titleTaskOld3 = findViewById(R.id.titleTask);
        SharedPreferences prefsTaskOld3 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userPurposeOld3 = prefsTaskOld3.getString("user_task_old3", "Нет занятия");

        titlePriceOld3 = findViewById(R.id.titlePrice);
        SharedPreferences prefsPriceOld3 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String priceTextOld3 = prefsPriceOld3.getString("price6", "Нет цены");

        titleTaskOld3.setText("Занятие: Динамическая аэробика");
        titlePriceOld3.setText("Цена: 499 рублей");

        titleTask4 = findViewById(R.id.titleTask);
        SharedPreferences prefsTask4 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userPurpose4 = prefsTask4.getString("user_task4", "Нет занятия");

        titlePrice4 = findViewById(R.id.titlePrice);
        SharedPreferences prefsPrice4 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String priceText4 = prefsPrice4.getString("price7", "Нет цены");

        titleTask4.setText("Занятие: Йога");
        titlePrice4.setText("Цена: 599 рублей");

        titleTaskOld4 = findViewById(R.id.titleTask);
        SharedPreferences prefsTaskOld4 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userPurposeOld4 = prefsTaskOld4.getString("user_task_old4", "Нет занятия");

        titlePriceOld4 = findViewById(R.id.titlePrice);
        SharedPreferences prefsPriceOld4 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String priceTextOld4 = prefsPriceOld4.getString("price8", "Нет цены");

        titleTaskOld4.setText("Занятие: Оздоровительная йога");
        titlePriceOld4.setText("Цена: 499 рублей");



        btnBack2 = findViewById(R.id.btnBack2);
        btnBack2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity6.this, ScreenActivity5.class);
                startActivity(intent);
            }
        });

        btnChooseSelf = findViewById(R.id.btnChooseSelf);
        btnChooseSelf.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity6.this, ScreenActivity8.class);
                startActivity(intent);
            }
        });

        btnContinue3 = findViewById(R.id.btnContinue3);
        btnContinue3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity6.this, ScreenActivity7.class);
                startActivity(intent);
            }
        });
    }
}

package com.example.modulefitness;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.appcompat.app.AppCompatActivity;

public class ScreenActivity7 extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Button btnBack3;
        Button btnWriting;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.screen7);

        btnBack3 = findViewById(R.id.btnBack3);
        btnBack3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity7.this, ScreenActivity6.class);
                startActivity(intent);
            }
        });

        btnWriting = findViewById(R.id.btnWriting);
        btnWriting.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity7.this, ScreenActivity9.class);
                startActivity(intent);
            }
        });
    }
}

package com.example.modulefitness;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.appcompat.app.AppCompatActivity;

public class ScreenActivity8 extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Button btnBack4;
        Button btnWriting2;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.screen8);

        btnBack4 = findViewById(R.id.btnBack4);
        btnBack4.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity8.this, ScreenActivity6.class);
                startActivity(intent);
            }
        });

        btnWriting2 = findViewById(R.id.btnWriting2);
        btnWriting2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity8.this, ScreenActivity9.class);
                startActivity(intent);
            }
        });
    }
}

package com.example.modulefitness;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.Spinner;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import org.w3c.dom.Text;

public class ScreenActivity9 extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Button btnExitAcc2;
        Button btnWriting3;

        TextView titleLoginSelf;
        TextView titleSelfGender;
        TextView titleSelfWeight;
        TextView titleSelfAge;
        TextView titlePurpose;
        Spinner listWriting;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.screen9);

        listWriting = findViewById(R.id.listWriting);
        String[] gender = {"форма", "1"};

        ArrayAdapter<String> adapter = new ArrayAdapter<>(
                this,
                android.R.layout.simple_spinner_item,
                gender
        );
        adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
        listWriting.setAdapter(adapter);

        listWriting.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                String selectedItem = gender[position];
                if (position != 0) {
                    Intent intent = new Intent(ScreenActivity9.this, ScreenActivity10.class);
                    startActivity(intent);
                }
            }
            @Override
            public void onNothingSelected(AdapterView<?> parent) {
                // ничего
            }
        });

        titleLoginSelf = findViewById(R.id.titleSelfLogin);
        SharedPreferences prefs = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userEnter = prefs.getString("user_enter", "Нет логина");

        titleSelfGender = findViewById(R.id.titleSelfGender);
        SharedPreferences prefs2 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userSelected = prefs.getString("user_selected", "Нет пола");

        titleSelfWeight = findViewById(R.id.titleSelfWeight);
        SharedPreferences prefs3 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userWeight = prefs.getString("user_weight", "Нет веса");

        titleSelfAge = findViewById(R.id.titleSelfAge);
        SharedPreferences prefs4 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userAge = prefs.getString("user_age", "Нет возраста");

        titlePurpose = findViewById(R.id.titleSelfPurpose);
        SharedPreferences prefs5 = getSharedPreferences("myPrefs", MODE_PRIVATE);
        String userPurpose = prefs.getString("user_purpose", "Нет цели");

        titleLoginSelf.setText("Логин: " + userEnter);
        titleSelfGender.setText("Пол: " + userSelected);
        titleSelfWeight.setText("Вес: " + userWeight);
        titleSelfAge.setText("Возраст: " + userAge);
        titlePurpose.setText("Цель: " + userPurpose);

        btnExitAcc2 = findViewById(R.id.btnExitAcc2);
        btnExitAcc2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity9.this, ScreenActivity1.class);
                startActivity(intent);
            }
        });

        btnWriting3 = findViewById(R.id.btnWriting3);
        btnWriting3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity9.this, ScreenActivity6.class);
                startActivity(intent);
            }
        });
    }
}

package com.example.modulefitness;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import androidx.appcompat.app.AppCompatActivity;

public class ScreenActivity10 extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Button btnCancelForm;
        Button btnExitForm;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.screen10);

        btnCancelForm = findViewById(R.id.btnCancelForm);
        btnCancelForm.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity10.this, ScreenActivity9.class);
                startActivity(intent);
            }
        });

        btnExitForm = findViewById(R.id.btnExitForm);
        btnExitForm.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(ScreenActivity10.this, ScreenActivity9.class);
                startActivity(intent);
            }
        });
    }
}

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

        <activity android:name=".ScreenActivity1"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

        <activity android:name=".ScreenActivity2"/>
        <activity android:name=".ScreenActivity3"/>
        <activity android:name=".ScreenActivity4"/>
        <activity android:name=".ScreenActivity5"/>
        <activity android:name=".ScreenActivity6"/>
        <activity android:name=".ScreenActivity7"/>
        <activity android:name=".ScreenActivity8"/>
        <activity android:name=".ScreenActivity9"/>
        <activity android:name=".ScreenActivity10"/>
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
    tools:context=".ScreenActivity1" >

    <TextView
        android:id="@+id/Name1"
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
        android:id="@+id/Name2"
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
        android:id="@+id/btnAuth"
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
        android:id="@+id/titleRegister"
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
        android:id="@+id/btnEnter"
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

    <Button
        android:id="@+id/btnHaveAcc"
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
        android:id="@+id/fieldPassword"
        android:layout_width="277dp"
        android:layout_height="54dp"
        android:ems="10"
        android:inputType="textPassword"
        android:minHeight="48dp"
        android:textColor="#F3835B"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:maxLength="12"
        app:layout_constraintVertical_bias="0.617"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <TextView
        android:id="@+id/titleLogin"
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
        app:layout_constraintVertical_bias="0.406"
        tools:ignore="MissingConstraints" />

    <EditText
        android:id="@+id/fieldLogin"
        android:layout_width="271dp"
        android:layout_height="48dp"
        android:digits="abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"
        android:ems="10"
        android:importantForAutofill="no"
        android:inputType="text"
        android:minHeight="48dp"
        android:textColor="#F3835B"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.478"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:maxLength="8"
        app:layout_constraintVertical_bias="0.464"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <TextView
        android:id="@+id/titlePassword"
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
        app:layout_constraintVertical_bias="0.546"
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
        android:id="@+id/titleLogin2"
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
        app:layout_constraintVertical_bias="0.406"
        tools:ignore="MissingConstraints" />

    <EditText
        android:id="@+id/fieldLogin2"
        android:layout_width="271dp"
        android:layout_height="48dp"
        android:digits="abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ"
        android:ems="10"
        android:importantForAutofill="no"
        android:inputType="text"
        android:minHeight="48dp"
        android:textColor="#F3835B"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.478"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:maxLength="12"
        app:layout_constraintVertical_bias="0.464"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <TextView
        android:id="@+id/titlePassword2"
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
        app:layout_constraintVertical_bias="0.546"
        tools:ignore="MissingConstraints" />

    <EditText
        android:id="@+id/fieldPassword2"
        android:layout_width="277dp"
        android:layout_height="54dp"
        android:ems="10"
        android:inputType="textPassword"
        android:minHeight="48dp"
        android:textColor="#F3835B"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:maxLength="12"
        app:layout_constraintVertical_bias="0.617"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <TextView
        android:id="@+id/titleAuthorization"
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
        android:id="@+id/btnEnter2"
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

    <Button
        android:id="@+id/btnGetAcc"
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

</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535">

    <TextView
        android:id="@+id/NameDuplic1"
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
        android:id="@+id/NameDuplic2"
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
        android:id="@+id/btnExitAcc"
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
        android:id="@+id/titleMenu"
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
        android:id="@+id/infoAddress"
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
        android:id="@+id/infoTime"
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
        android:id="@+id/infoPhone"
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
        android:id="@+id/btnContinue"
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
    android:background="#353535"
    tools:layout_editor_absoluteX="0dp"
    tools:layout_editor_absoluteY="-31dp">

    <TextView
        android:id="@+id/hintAge"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Укажите Ваш возраст"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.306"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.747"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titleAge"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Возраст:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.228"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.697"
        tools:ignore="MissingConstraints" />

    <EditText
        android:id="@+id/fieldAge"
        android:layout_width="103dp"
        android:layout_height="48dp"
        android:maxLength="3"
        android:digits="1234567890"
        android:ems="10"
        android:importantForAutofill="no"
        android:inputType="text"
        android:minHeight="48dp"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.538"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.705"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <TextView
        android:id="@+id/hintGender"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Выбор пола"
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
        android:id="@+id/titleGender"
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

    <TextView
        android:id="@+id/titleWeight"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Вес:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.202"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.471"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnContinue2"
        android:layout_width="175dp"
        android:layout_height="61dp"
        android:layout_marginHorizontal="8dp"
        android:layout_marginTop="64dp"
        android:backgroundTint="#000000"
        android:text="Продолжить"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.873"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <Button
        android:id="@+id/btnBack"
        android:layout_width="187dp"
        android:layout_height="52dp"
        android:layout_marginHorizontal="8dp"
        android:layout_marginTop="64dp"
        android:backgroundTint="#000000"
        android:text="Вернуться назад"
        android:textColor="#F3835B"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.023"
        tools:ignore="HardcodedText,MissingConstraints" />

    <TextView
        android:id="@+id/titleCharacteristic"
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
        android:id="@+id/listGender"
        android:layout_width="147dp"
        android:layout_height="48dp"
        android:spinnerMode="dropdown"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.352" />

    <EditText
        android:id="@+id/fieldWeight"
        android:layout_width="103dp"
        android:layout_height="48dp"
        android:maxLength="3"
        android:digits="1234567890"
        android:ems="10"
        android:importantForAutofill="no"
        android:inputType="text"
        android:minHeight="48dp"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.428"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.471"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <TextView
        android:id="@+id/hintWeight"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Напишите Ваш вес"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.279"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.521"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/hintPurpose"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Напишите Вашу цель занятия"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.405"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.638"
        tools:ignore="MissingConstraints" />

    <EditText
        android:id="@+id/fieldPurpose"
        android:layout_width="103dp"
        android:layout_height="48dp"
        android:maxLength="15"
        android:ems="10"
        android:importantForAutofill="no"
        android:inputType="text"
        android:minHeight="48dp"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.467"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.592"
        tools:ignore="MissingConstraints,SpeakableTextPresentCheck" />

    <TextView
        android:id="@+id/titlePurpose"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Цель:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.21"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.589"
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
        android:id="@+id/hintDescTask"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Предлагаемое занятие"
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
        android:id="@+id/btnContinue3"
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
        android:id="@+id/btnBack2"
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
        android:id="@+id/titleTasks"
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
        android:id="@+id/titlePrice"
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
        android:id="@+id/titleTask"
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
        android:id="@+id/hintPrice"
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
        android:id="@+id/titleDesc"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Исходя из Вашего веса, цели и возраста"
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
        android:id="@+id/titleDesc2"
        android:layout_width="311dp"
        android:layout_height="31dp"
        android:text="было подобрано следующее занятие:"
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
        android:id="@+id/btnChooseSelf"
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
        android:id="@+id/hintTime"
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
        android:id="@+id/hintTrainer"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ведущий занятия"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.15"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.549"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/hintPinTask"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Запланированное занятие"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.188"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.422"
        tools:ignore="MissingConstraints" />

    <EditText
        android:id="@+id/fieldTime"
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
        android:id="@+id/titleTime"
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
        android:id="@+id/btnWriting"
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
        android:id="@+id/btnBack3"
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
        android:id="@+id/titleWriting"
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
        android:id="@+id/titleTrainer"
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
        android:id="@+id/titleTask2"
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
        android:id="@+id/btnWriting2"
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
        android:id="@+id/fieldTime2"
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
        android:id="@+id/hintTime2"
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
        android:id="@+id/titleTime2"
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
        android:id="@+id/btnBack4"
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
        android:id="@+id/tilteSelfWriting"
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
        android:id="@+id/hintChooseTrainer"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Выбор тренера"
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
        android:id="@+id/listTrainer"
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
        android:id="@+id/titleTrainer2"
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
        android:id="@+id/hintChooseTask"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Выбор занятия"
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
        android:id="@+id/titleTask3"
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
        android:id="@+id/listTask"
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
    android:background="#353535"
    tools:layout_editor_absoluteX="22dp"
    tools:layout_editor_absoluteY="11dp">

    <TextView
        android:id="@+id/hintSelfPurpose"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ваша цель"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.057"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.856"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titleSelfPurpose"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Цель:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.054"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.822"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/hintSelfAge"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ваш возраст"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.057"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.767"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titleSelfLogin"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Логин:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.056"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.453"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/hintSelfLogin"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ваш логин"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.054"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.488"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titleSelfGender"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Пол:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.053"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.545"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/hintSelfGender"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ваш пол"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.057"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.581"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titleSelfWeight"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Вес:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.047"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.637"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/hintSelfWeight"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ваш вес"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.051"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.671"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titleSelfAge"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Возраст:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.054"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.734"
        tools:ignore="MissingConstraints" />

    <Spinner
        android:id="@+id/listWriting"
        android:layout_width="147dp"
        android:layout_height="48dp"
        android:spinnerMode="dropdown"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.598"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.344" />

    <TextView
        android:id="@+id/titleSelfTask"
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
        app:layout_constraintVertical_bias="0.342"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/hintSelfTasks"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ваши записи"
        android:textColor="#ADADAD"
        android:textSize="16sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.063"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.394"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnWriting3"
        android:layout_width="234dp"
        android:layout_height="62dp"
        android:layout_marginHorizontal="8dp"
        android:layout_marginTop="64dp"
        android:backgroundTint="#000000"
        android:text="Записаться снова"
        android:textColor="#F3835B"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.934"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <Button
        android:id="@+id/btnExitAcc2"
        android:layout_width="187dp"
        android:layout_height="52dp"
        android:layout_marginHorizontal="8dp"
        android:layout_marginTop="64dp"
        android:backgroundTint="#000000"
        android:text="Выйти из системы"
        android:textColor="#0077FF"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.023"
        tools:ignore="HardcodedText,MissingConstraints" />

    <TextView
        android:id="@+id/titleSelfAccount"
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

</androidx.constraintlayout.widget.ConstraintLayout>

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#353535"
    tools:layout_editor_absoluteX="0dp"
    tools:layout_editor_absoluteY="-8dp">

    <TextView
        android:id="@+id/hintTrainerForm"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Ведущий занятия"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.202"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.484"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titleTrainerForm"
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
        android:id="@+id/hintTimeForm"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Время записи"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.185"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.595"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titleTimeForm"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Время:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.172"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.549"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titlePriceForm"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Цена:"
        android:textColor="#F3835B"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.165"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.651"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/hintPriceForm"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Стоимость занятия"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.21"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.7"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/hintTaskForm"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Запланированное занятие"
        android:textColor="#ADADAD"
        android:textSize="14sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.251"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.383"
        tools:ignore="MissingConstraints" />

    <TextView
        android:id="@+id/titleTaskForm"
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
        app:layout_constraintVertical_bias="0.332"
        tools:ignore="MissingConstraints" />

    <Button
        android:id="@+id/btnExitForm"
        android:layout_width="224dp"
        android:layout_height="59dp"
        android:layout_marginHorizontal="8dp"
        android:layout_marginTop="64dp"
        android:backgroundTint="#000000"
        android:text="Закрыть форму"
        android:textColor="#0077FF"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.918"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <Button
        android:id="@+id/btnCancelForm"
        android:layout_width="143dp"
        android:layout_height="58dp"
        android:layout_marginHorizontal="8dp"
        android:layout_marginTop="64dp"
        android:backgroundTint="#000000"
        android:text="Отменить"
        android:textColor="#FF0000"
        android:textSize="20sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.059"
        app:layout_constraintHorizontal_weight="1"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.916"
        tools:ignore="DuplicateIds,MissingConstraints" />

    <TextView
        android:id="@+id/titleForm"
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
        android:id="@+id/titleNumberForm"
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

plugins {
    alias(libs.plugins.android.application)
}

android {
    namespace = "com.example.modulefitness"
    compileSdk = 35

    defaultConfig {
        applicationId = "com.example.modulefitness"
        minSdk = 21
        targetSdk = 35
        versionCode = 1
        versionName = "1.0"

        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            isMinifyEnabled = false
            proguardFiles(
                getDefaultProguardFile("proguard-android-optimize.txt"),
                "proguard-rules.pro"
            )
        }
    }
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_11
        targetCompatibility = JavaVersion.VERSION_11
    }
}

dependencies {

    implementation(libs.appcompat)
    implementation(libs.material)
    implementation(libs.activity)
    implementation(libs.constraintlayout)
    implementation(libs.androidx.constraintlayout)
    testImplementation(libs.junit)
    androidTestImplementation(libs.ext.junit)
    androidTestImplementation(libs.espresso.core)
}

dependencies {
    implementation("com.squareup.okhttp3:okhttp:4.10.0")
    implementation("org.json:json:20230227")
}
