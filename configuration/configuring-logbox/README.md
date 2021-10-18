# Configuring LogBox

No matter what configuration you decide to use, you will always have to instantiate LogBox with a `LogBoxConfig` object: `logbox.system.logging.config.LogBoxConfig`. However you have the option of either talking directly to this CFC or creating a more portable configuration. This portable configuration we denote as a simple data CFC that contains the LogBox configuration data using what we call our **LogBox DSL** (Domain Specific Language).

The cool thing about this LogBox DSL is that it is exactly the same whether you are using LogBox in ColdBox applications or in any other framework or non-framework ColdFusion application. So you can configure LogBox by:

1. Creating a portable data CFC using the LogBox DSL or
2. Creating the `LogBoxConfig` object and interacting with its methods
