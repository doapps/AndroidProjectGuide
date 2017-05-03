# Buenas prácticas de desarrollo Android

A continuación encontrarán una serie de buenas prácticas a tomar en cuenta para a la hora de programar aplicaciones móviles
para las plataformas Android.
Como bien sabemos a la hora de desarrollar aplicaciones nativas para Android, usamos el lenguaje de programación Java y en esta
ocación el IDE oficial Android Studio.
Si bien Android Studio nos ofrece de por defecto la estructura general del proyecto, a medida que vayamos profundizando en el desarrollo
de una aplicación o vayamos creando aplicaciones más complejas necesitaremos crear un código entendible por cualquier miembro del equipo,
un código modular que pueda ser escalable fácilmente y por sobre todo un código limpio basándonos en estándares de programación que
solo los buenos desarrolladores siguen.


https://github.com/futurice/android-best-practices
https://github.com/futurice/android-best-practices/tree/master/templates/rx-architecture


## Estructura del proyecto

Esta es la estructura base que nos proporciona Android Studio al crear un proyecto para aplicaciones móviles.

```
├─ app
│  ├─ libs
│  ├─ src
│  │  ├─ androidTest
│  │  │  └─ java
│  │  │     └─ com/domain/project
│  │  └─ main
│  │     ├─ java
│  │     │  └─ com/domain/project
│  │     ├─ res
│  │     └─ AndroidManifest.xml
│  ├─ build.gradle
│  └─ proguard-rules.pro
├─ build.gradle
└─ settings.gradle
```


### Estructura /java

> **Nota:**
>
> - El paquete **java** es un contenedor de clases para diferentes fines dentro de la aplicación.
> - El IDE Android Studio provee por defecto las carpetas bases.
> - Si un paquete contiene sub carpetas solo valdrá la pena crear las carpetas si estas contienen clases.
> - Las carpetas debe estar en minuscula y en singular.

```
├─ java
│  ├─ com.domain.project
│     ├─ activity
│     ├─ fragment
│     ├─ application
│     ├─ model
│     ├─ adapter
│     ├─ config
│     ├─ dialog
│     ├─ listener
│     ├─ networking
│     ├─ database
│     ├─ session
│     ├─ util
│     └─ widget

```


##### Estructura /java/activity
```
├─ java
│  ├─ com.domain.project
│     └─ activity
│         └─ MainActivity.java
│         └─ SplashActivity.java

** En caso amerite se crearán subcarpetas a discreción del desarrollador para ordenar las clases.
```

##### Estructura /java/fragment
```
├─ java
│  ├─ com.domain.project
│     └─ fragment
│         └─ MainFragment.java

** En caso amerite se crearán subcarpetas a discreción del desarrollador para ordenar las clases.
```

#### Estructura /java/application
```
├─ java
│  ├─ com.domain.project
│     └─ applicaction
│         └─ MainApplication.java

** En caso amerite se crearán subcarpetas a discreción del desarrollador para ordenar las clases.
```

#### Estructura /java/model
```
├─ java
│  ├─ com.domain.project
│     └─ model
│         └─ Product.java

```

#### Estructura /java/adapter
```
├─ java
│  ├─ com.domain.project
│     └─ adapter
│         └─ ProductAdapter.java

** Importante considerar que el nombre del adapter tiene que ser equivalente al nombre del modelo
```

#### Estructura /java/config
```
├─ java
│  ├─ com.domain.project
│     └─ config
│         └─ Setting.java
│         └─ Message.java

** Almacenar variables staticas y finales que puedan ser reutilizables como mensajes dinámicos, log errores, etc.
```

#### Estructura /java/dialog
```
├─ java
│  ├─ com.domain.project
│     └─ dialog
│         └─ ProgressDialog.java

** Almacenar las clases controladoras de diálogos customizados.
```

#### Estructura /java/listener
```
├─ java
│  ├─ com.domain.project
│     └─ listener
│         └─ NotificationListener.java

** Almacenar las clases de tipo interface
```

#### Estructura /java/networking
```
├─ java
│  ├─ com.domain.project
│     └─ networking
│         └─ connection
│             └─ RestApi.java
│         └─ fcm
│             └─ InstanceService.java
│             └─ MessagingService.java
│         └─ background
│             └─ TrackerService.java
│             └─ SyncronizeService.java

** connection Almacenar las clases que involucran a Retrofit
** fcm las clases firebase
** background otras clases en segundo plano.
```

#### Estructura /java/database
```
├─ java
│  ├─ com.domain.project
│     └─ database
│         └─ SQLiteConnection.java
│         └─ TableContent.java
│         └─ table
│              └─ EntityTable.java
│         └─ process
│              └─ EntityInterface.java
│              └─ EntityProcessor.java


** ProductTable.java define el nombre de la tabla y las columnas.
** SQLiteConnection.java hereda de SQLiteOpenHelper y define la creación o actualización de la base de datos.
** TableContent.java contiene el script de las tablas, que serán llamadas desde la clase SQLiteConnection.java
PENDIENTE EXPERIMENTAR
```

#### Estructura /java/session
```
├─ java
│  ├─ com.domain.project
│     └─ session
│         └─ Preference.java

** Almacenar las clases de tipo preferens asociados al usuario
```


#### Estructura /java/util
```
├─ java
│  ├─ com.domain.project
│     └─ util
│         └─ InternetUtil.java
│         └─ ValidatorUtil.java

** Almacenar las clases de tipo utilería
```

#### Estructura /java/widget
```
├─ java
│  ├─ com.domain.project
│     └─ widget
│         └─ BoldButton.java
│         └─ RegularText.java

** Almacena componentes visuales customizados
```


### Estructura JAVA

#### Nomenclatura de paquetes
Los paquetes se nombran en singular y con letras minúsculas.
```
activity
fragment
adapter
model
util
```

#### Nomenclatura de clases
Las clases java se nombran utilizando el estándar “UpperCamelCase”, es decir utilizando
una combinación de palabras que empiezan con mayúscula como “ClasePrincipal”.
```
MainActivity
LoginActivity
RegisterFragment
DetailFragment
```

### Estructura de un activity
```java

public class ExampleActivity extends AppCompatActivity {

    @BindView(R.id.global_image)
    ImageView global_image;

    Toolbar toll;

    private int cont;
    private String user;
    private double total;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_detalle_quota);

        ButterKnife.bind(this);

        getToolbar();
        DesignUtil.customStatusBarColor(getWindow(), this, R.color.smv_plomo2_3);
    }


    /**
     * Void que se encarga de los detalles del toolbar
     */
    private void getToolbar() {

        toll = (Toolbar) findViewById(R.id.toolbar);

        setSupportActionBar(toll);
        DesignUtil.toolbarColor(toll, this, R.color.smv_plomo2_3);
        getSupportActionBar().setTitle("");
        getSupportActionBar().setDisplayHomeAsUpEnabled(true);

        toll.setNavigationOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finish();
            }
        });
    }

    @OnClick(R.id.image_global)
    public void getAddProdafolio() {
        startActivity(new Intent(this, BienvenidoActivity.class));
        overridePendingTransition(R.anim.fade_in, R.anim.fade_out);
    }

    /*********************************************************************************************/

    private void getToolbar() {
            Toolbar toll = (Toolbar) findViewById(R.id.toolbar);

            DesignUtil.toolbarTransparent(toll);
            setSupportActionBar(toll);
            getSupportActionBar().setTitle("");
            getSupportActionBar().setDisplayHomeAsUpEnabled(true);
        }

        @OnClick(R.id.button_opcion1)
        public void getOption1() {
            isEstado(1);
            include_opcion1.setVisibility(View.VISIBLE);
            include_opcion2.setVisibility(View.INVISIBLE);
        }

        @OnClick(R.id.button_opcion2)
        public void getOption2() {
            isEstado(2);
            include_opcion1.setVisibility(View.INVISIBLE);
            include_opcion2.setVisibility(View.VISIBLE);
        }

        /**
         * Metodo cambia los colores de los botones
         *
         * @param status :
         *               <p>
         *               1 -> Color de selecion en el botton 1
         *               2 -> Color de selecion en el botton 2
         */

        public void isEstado(int status) {
            if (status == 1) {
                button_opcion1.setBackground(getResources().getDrawable(R.drawable.borde_in_1));
                button_opcion1.setTextColor(getResources().getColor(R.color.smv_plomo2));

                button_opcion2.setBackground(getResources().getDrawable(R.drawable.borde_of_1));
                button_opcion2.setTextColor(getResources().getColor(R.color.smv_blanco));
            } else {
                button_opcion1.setBackground(getResources().getDrawable(R.drawable.borde_of_2));
                button_opcion1.setTextColor(getResources().getColor(R.color.smv_blanco));

                button_opcion2.setBackground(getResources().getDrawable(R.drawable.borde_in_2));
                button_opcion2.setTextColor(getResources().getColor(R.color.smv_plomo2));
            }
        }

}

### Comentar una clases
```java
/**
  * Initializing GUI
  **/
private void init() {
    Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
    TextView text = (TextView) findViewById(R.id.text);
}
```

### Estructura RES

#### Nomenclatura de paquetes
Al igual que en la sección Java, también se nombran los paquetes en minúsculas pero
no siempre en singular, habrá casos en los que usemos plurales como la carpeta “values”
y otros casos donde se usan guiones como en el caso de crear carpetas para para soporte de
de versiones android como “values-v21”.
```
drawable
layout
manu
values
values-v21
```

### Definir formato de Colors.xml

```xml
<resources>
    <color name="colorPrimary">@color/black</color>
    <color name="colorPrimaryDark">@color/green</color>
    <color name="colorAccent">@color/white</color>

    <!-- basic colors -->
    <color name="white">#FFFFFF</color>
    <color name="black">#000000</color>
    <color name="green">#27D34D</color>
    <color name="blue">#2A91BD</color>
    <color name="orange">#FF9D2F</color>
    <color name="red">#FF432F</color>

    <!-- opacity white -->
    <color name="white_100">#00FFFFFF</color>
    <color name="white_75">#BFFFFFFF</color>
    <color name="white_50">#80FFFFFF</color>
</resources>
```

### Definir cadenas estáticas por pantalla en strings.xml

```xml
<resources>
    <string name="app_name">DoApps</string>
    <!-- activity_menu -->
    <string name="menu_home">Inicio</string>
    <string name="menu_contact">Contactos</string>
    <string name="menu_profile">Perfil</string>
    <!-- fragment_profile -->
    <string name="label_lastname">Apellido</string>
    <string name="label_name">Nombre</string>
</resources>
```

#### Uso de las carpetas “mipmap“ y “drawable”
Android Studio nos provee por defecto de ambas carpetas para almacenar los recursos gráficos del proyecto.

La carpeta `mipmap`, sirve exclusivamente para almacenar el icon launcher de la aplicación, es decir que solo
almacenará los archivos `ic_launcher.png` y su distribución será así:
```
├─ mipmap-hdpi
│  ├─ ic_launcher.png
│  |
├─ mipmap-mdpi
│  ├─ ic_launcher.png
│  |
├─ mipmap-xhdpi
│  ├─ ic_launcher.png
│  |
├─ mipmap-xxhdpi
│  ├─ ic_launcher.png
│  |
├─ mipmap-xxxhdpi
│  ├─ ic_launcher.png
│  |
```

La carpeta `drawable`, sirve para almacenar recursos .xml tales como los selector, shape y derivados.
La carpeta `drawable-hdpi`, `drawable-xhdpi`y demás sirven para almcenar los recursos gráficos de la aplicación, como íconos, logos, imágenes de fondo, etc.

#### Utilizar fuentes de texto
Si bien Androi Studio no nos provee de una carpeta por defecto para almacenar archivos .ttf .otf o derivados, podemos optar por crear nuestra propia
paquetería para almacenar otros archivos que no sea recursos gráficos.

Crearemos una carpeta llamanda `assets` y dentro crearemos la carpeta `font`, aquí podremos guardar nuestros archivos .ttf o derivados.

```
─ main
   ├─ assets
   │  └─ font
   ├─ java
   │  └─ com/domain/project
   ├─ res
   └─ AndroidManifest.xml
```

### Crear tus componentes customizados (widgets)

## TextView customizados


Utilitarios
-----------

### Crea tus utilitarios
A medida que ganamos experiencia como desarrolladores, generamos código que puede ser reutilizable los más comunes
son los utilitarios, pequeñas clases con funciones específicas como por ejemplo un utilitario cuyo único objetivo es
retornar la cantidad de días que han transcurrido desde el origen del mundo hasta la fecha de hoy.

```
─ main
   ├─ assets
   │  └─ font
   ├─ java
   │  └─ com/domain/project
   │     └─ activity
   │     └─ fragment
   │     └─ util
   ├─ res
   └─ AndroidManifest.xml
```
