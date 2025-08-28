init:
	docker compose exec app composer install
	docker compose exec app npm install
	docker compose exec app php artisan storage:link
	docker compose exec app chmod -R 775 storage resources
	docker compose exec app chown -R $(shell id -u):www-data /var/www/src
	docker compose exec app php artisan key:generate
	docker compose exec app php artisan migrate
	docker compose exec app php artisan config:clear
	docker compose exec app npm run dev
start:
	docker compose exec app php artisan config:clear
	docker compose exec app npm run dev
updateReset:
	docker compose exec app composer install
	docker compose exec app npm install
	docker compose exec app chmod -R 775 storage resources
	docker compose exec app chown -R $(shell id -u):www-data /var/www/src
	docker compose exec app php artisan config:clear
	docker compose exec app make cacheReset
	docker compose exec app npm run build
permissionReset:
	docker compose exec app chown -R $(shell id -u):www-data /var/www/src
