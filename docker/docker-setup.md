# Build Image

```bash
docker build -t local-api-qm-new -f docker/Dockerfile --build-arg DEMO_USERNAME=BDou01 --build-arg DEMO_PASSWORD=bdou2021 .
```

# Build Container
```bash
docker run -d --name local-api-qm-new-con -p 4440:443 -v "$(pwd)":/var/www/html local-api-qm-new
```

# Reset json cache
```
git checkout qsmodule/research/functions/json/cache
```

# Reset theme cache
```
git checkout qsmodule/research/assets/css/theme_cache
```