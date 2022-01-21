# Laravel failing with missing SQL Driver in Azure App Service

I worked on Laravel framework when the customer was seen an error as mentioned below.<br>
The customer used PHP/7.4 and the App was connecting to DB.  <br>
However, the issue was seen because of missing DB driver.<br>
The customer used GitHub Action for building & deploying.<br>

Error: <br>

 > Illuminate\Foundation\ComposerScripts::postAutoloadDump<br>
  > @php artisan package:discover --ansi<br>
    
   Illuminate\Database\QueryException <br>
  
 could not find driver (SQL: select * from information_schema.tables where table_schema = hiring and table_name = app_types and table_type = 'BASE TABLE')<br>
    
   at vendor/laravel/framework/src/Illuminate/Database/Connection.php:703<br>
       699â–•         // If an exception occurs when attempting to run a query, we'll format the error<br>
      700â–•         // message to include the bindings with SQL, which will make this exception a<br>
      701â–•         // lot more helpful to the developer instead of just the database's errors.<br>
       702â–•         catch (Exception $e) {<br>
      âžœ 703â–•             throw new QueryException(<br>
        704â–•                 $query, $this->prepareBindings($bindings), $e<br>
        705â–•             );<br>
        706â–•         }<br>
        707â–•     }<br>
    
    1   [internal]:0<br>
         Illuminate\Foundation\Application::Illuminate\Foundation\{closure}(Object(App\Providers\AppServiceProvider))<br><br>
   


Resolution: <br>
The resolution to the issue was added into workflow/ .yaml file the extensions:( see workflow/.yaml for more details ) <br>
 extensions: mbstring,PDO,grpc,tokenizer,xml,json,ctype,fileinfo,openssl,bcmath,mysql<br>
 
 NOTE: You can change DB setting from .env.example file
 
 

