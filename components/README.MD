For start symple server:
node -e "require('express')().use(require('express').static(__dirname, {index:'index.html'})).listen(8181)"