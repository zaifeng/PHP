apc安装前提PHP版本必须是**5.4 or older**

	wget http://pecl.php.net/get/APC-3.1.13.tgz
	tar xf APC-3.1.13.tgz
	cd APC-3.1.13/
	/usr/local/php/bin/phpize
	./configure --enable-apc --enable-apc-mmap --with-php-config=/usr/local/php/bin/php-config
	make
	make install make
