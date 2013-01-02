#CakePHP 2.x RememberMe Component

Currently this is a very basic component that will handle a lot of cookie handling when dealing with autologins and CakePHP's Auth. The component takes in an array of the user's details and sets it into a cookie to use for future login attempts.

##Installation
Install the plugin:

	cd myapp
	git submodule add git://github.com/walker/remember_me.git app/Plugin/RememberMe

Depending on which user controller you would like the RememberMe functions to work on, open up the controller and type in.

	public $components = array('RememberMe.RememberMe');

In order to log a user in and set the cookie information you can use something like this in your login action in your controller:

	function members_login() {
		if ($this->Auth->user()) {
			if (!empty($this->data)) {
				$this->RememberMe->setRememberMe($this->data[$this->Member->alias]);
			}
			$this->redirect($this->Auth->loginRedirect);
		}
	}

##Refresh Cookie Expiry Times

Keeping cookie expiry dates in relation to the user's last action can be done in the AppController using the checkUser method in RememberMe. For example you may like to place it in your AppController like:

	function _rememberMember() {
		if ($this->params['action'] != 'members_logout') {
			$this->RememberMe->checkUser();
		}
	}
