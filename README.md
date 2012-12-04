# PHP Presenters

It's very easy to end up with complicated, brittle views full of messy logic and presentation code that really should be somewhere else. In my book, [The CodeIgniter Handbook - Volume One - Who Needs Ruby?](https://efendibooks.com/books/codeigniter-handbook/vol-1) I discuss a great technique for cleaning up your views.

This small library is a lightweight, tested solution for using presenters within PHP (and CodeIgniter apps). **This library is tailored for CI, but works with any PHP application.**

## Synopsis

	class Book_Presenter extends Presenter
	{
		public function price()
		{
			return number_format($this->book->price, 2);
		}
	}

	$book = $this->db->where('id', 1)->get('books')->row();
	$book = new Book_Presenter($book);

	echo $book->title() . ' costs ' . $book->price();

## Installation

Add it to your **composer.json**:

	{
		"require": {
			"jamierumbelow/presenters": "*"
		}
	}

Run `composer update`:

	$ php composer.phar update

...and autoload:

	require_once 'vendor/autoload.php';

## Usage

Create a new class with the suffix `_Presenter`. `Book_presenter` will create a `$this->book` variable, `Game_Type_Presenter` will create a `$this->game_type` variable.

Instantiate a new presenter object and pass through the raw object:

	$book = $this->db->where('id', 1)->get('books')->row();
	$book = new Book_Presenter($book);

You can then access the data inside the presenter:

	class Book_Presenter extends Presenter
	{
		public function title()
		{
			return $this->book->title . ' - ' . $this->book->subtitle;
		}
	}

If you'd like to customise the object name, pass it through as the second parameter:

	$book = new Book_Presenter($book, 'bookObject');

	class Book_Presenter extends Presenter
	{
		public function title()
		{
			return $this->bookObject->title . ' - ' . $this->bookObject->subtitle;
		}
	}