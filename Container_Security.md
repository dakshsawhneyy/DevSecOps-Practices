<img width="451" height="325" alt="image" src="https://github.com/user-attachments/assets/5dd6d667-7198-4593-82ac-72c1fbfc9047" />

```
FROM node:25
WORKDIR /app
# Create non-root user
RUN groupadd -r appuser && useradd -r -g appuser appuser
COPY . .
RUN npm install
# Switch to non-root user
USER appuser
EXPOSE 3000
CMD ["npm", "start"]
```

<img width="694" height="589" alt="image" src="https://github.com/user-attachments/assets/80c3b010-40c5-4fbf-8746-aa4417c56423" />

### Harden the Runtime (Defense in Depth)
```
docker run \
  --read-only \
  --tmpfs /tmp \
  --cap-drop ALL \
  --security-opt no-new-privileges \
  --pids-limit 100 \
  --memory 256m \
  --cpus 0.5 \
  -p 3000:3000 \
  secure-app
```
