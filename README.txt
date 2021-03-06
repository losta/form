Form

A lightweight framework for defining, validating and rendering HTML forms.


OVERVIEW

Form lets you define forms by subclassing a base Form class. You specify
the action, method etc. of the form, and override a class method that returns
an array defining all the fields of your form.

Defining, validating and rendering HTMl forms basically comes down to
three areas:

  * Validation of form data.
  * Rendering of input elements.
  * Displaying error messages when user input is invalid.

Form has built-in support for validation of standard types of input data
like e-mail addresses, URLs, timestamps, integers etc. For special cases,
adding validation rules is as simple (or hard) as writing a regular expression
or writing a callback function.

The same goes for rendering standard input fields; there is built-in support
for rendering fields as text inputs, select drop-downs, checkboxes,
radio buttons, textareas etc., and defining custom rendering is simple.

Error messages are designed to be sensible by default, and easy to customize.

See "Installation and usage" below for a very minimal example. Check out the
demos at http://david.hgbrg.se/form/doc/ for a quick overview.


INSTALLATION AND USAGE

Install by copying lib/form.php and lib/form/ to a sensible directory.
Include lib/form.php and you are ready to go.

A small example:

<?php

require 'lib/form.php';

/** A minimal form example. */
class Simple_form extends Form
{
  public $form_action = 'target.php';
  public $form_method = 'post';

  /** Returns a definition of the fields of this form. */
  protected function fields()
  {
    return array(
      'name' => array(
        'label' => 'Please enter your name',
        'type' => 'string',
        'required' => true, # the user must fill in this field
        'render_as' => 'text',
      ),
      'submit' => true, # will use default submit button
    );
  }
}

$form = new Simple_form();

if ( $_SERVER['REQUEST_METHOD'] == 'POST' ) {
  # need to tell the form what data source to use
  $form->source( $_POST );
  if ( $form->is_valid() )
    echo 'OK!';
  else
    echo 'Uh-oh!';
}

echo $form->render();

?>


DOCUMENTATION AND DEMOS

Latest source code and documentation available at http://github.com/dfh/form/

Documentation can also be found in the doc/ folder.

Demos and documentation available at http://david.hgbrg.se/form/


KNOWN ISSUES

Theses names are reserved (due to implementation choices) and not possible to
use as field names:

  form_action
  form_method
  form_enctype
  form_accept_charset
  template_dir
  anything prefixed by underscore ("_")


META

Copyright 2010, 2011 David Högberg (david@hgbrg.se, http://david.hgbrg.se)

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
