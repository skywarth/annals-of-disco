### "Maximum execution time of 30 seconds exceeded"
Possible solutions:
- Increase ```max_execution_time``` in ```php.ini```
- Increase ```max_file_uploads``` in ```php.ini```
- ```set_time_limit(10000);``` before the bugging section begins
- If it is a job; run the queue using ```php artisan queue:work --timeout=0```
