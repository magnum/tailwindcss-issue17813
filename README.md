# tailwindcss-issue17813
https://github.com/tailwindlabs/tailwindcss/issues/17813#issuecomment-2847408119

This repository is intended to test a reported issue with Tailwind CSS when used in a Rails application with Kamal for deployment. It has been alleged that certain utility classes, such as `py-2`, throw an error when building the Docker image on macOS and/or are absent from the final production CSS.


**Steps to Reproduce:**
* Clone the repository.
* Install the required libraries using `bundle`.
* Start the application with `bin/dev`.
* Visit `http://localhost:3000/` to view a test page in development (the `px-2` utility is functioning).
* Return to the shell and execute `kamal build dev`; an error will be thrown.
```
...
#17 2.116 Tasks: TOP => assets:precompile => tailwindcss:build
#17 2.116 (See full trace by running task with --trace)
#17 ERROR: process "/bin/sh -c SECRET_KEY_BASE_DUMMY=1 ./bin/rails assets:precompile" did not complete successfully: exit code: 1
------
 > [build 6/6] RUN SECRET_KEY_BASE_DUMMY=1 ./bin/rails assets:precompile:
2.098 Error: Cannot apply unknown utility class: px-2
2.105 bin/rails aborted!
2.105 Command failed with exit 1: /usr/local/bundle/ruby/3.3.0/gems/tailwindcss-ruby-4.1.4-x86_64-linux-gnu/exe/x86_64-linux-gnu/tailwindcss
2.116 
2.116 Tasks: TOP => assets:precompile => tailwindcss:build
2.116 (See full trace by running task with --trace)
------
Dockerfile:49
--------------------
  47 |     
  48 |     # Precompiling assets for production without requiring secret RAILS_MASTER_KEY
  49 | >>> RUN SECRET_KEY_BASE_DUMMY=1 ./bin/rails assets:precompile
  50 |     
  51 |     
--------------------
ERROR: failed to solve: process "/bin/sh -c SECRET_KEY_BASE_DUMMY=1 ./bin/rails assets:precompile" did not complete successfully: exit code: 1
´´´