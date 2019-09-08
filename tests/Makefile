
PROJECT_DIR = $(realpath $(CURDIR)/../)

init-selenium:
	docker-compose -f $(PROJECT_DIR)/Docker/docker-compose.yml up --build -d selenium-chrome
	sleep 2

stop-selenium:
	-docker-compose -f $(PROJECT_DIR)/Docker/docker-compose.yml down

test-all:
	$(MAKE) test-acceptance
	$(MAKE) test-functional
	$(MAKE) test-unit

test-acceptance: init-selenium
	-docker-compose -f $(PROJECT_DIR)/Docker/docker-compose.yml run --rm codecept run acceptance -d --html
	$(MAKE) stop-selenium

test-functional: init-selenium
	-docker-compose -f $(PROJECT_DIR)/Docker/docker-compose.yml run --rm codecept run functional -d --html
	$(MAKE) stop-selenium

test-unit: init-selenium
	-docker-compose -f $(PROJECT_DIR)/Docker/docker-compose.yml run --rm codecept run unit -d --html
	$(MAKE) stop-selenium
