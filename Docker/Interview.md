# Docker Basic Interview Questions (100 Q&A)

## Docker Fundamentals

1. What is Docker?  
   Docker is a containerization platform used to package applications and their dependencies into containers.

2. What is a container?  
   A container is a lightweight, standalone environment that runs an application.

3. What is a Docker image?  
   A Docker image is a blueprint used to create containers.

4. Difference between container and image?  
   Image is a template; container is a running instance of that image.

5. What is Docker Engine?  
   Docker Engine is the core service that builds and runs containers.

### Installation & Commands

6. Command to check Docker version?  
   `docker --version`

7. Command to pull an image?  
   `docker pull nginx`

8. Command to run a container?  
   `docker run nginx`

9. List running containers?  
   `docker ps`

10. List all containers?  
    `docker ps -a`

### Container Management

11. Stop a container?  
    `docker stop <container_id>`

12. Start a container?  
    `docker start <container_id>`

13. Remove a container?  
    `docker rm <container_id>`

14. Remove an image?  
    `docker rmi <image_id>`

15. Run container in background?  
    `docker run -d nginx`

### Dockerfile

16. What is a Dockerfile?  
    A file containing instructions to build a Docker image.

17. Command to build image?  
    `docker build -t myapp .`

18. FROM instruction?  
    Defines base image.

19. RUN instruction?  
    Executes commands during build.

20. CMD instruction?  
    Specifies default command to run container.

### Networking

21. What is Docker networking?  
    It allows containers to communicate with each other.

22. Default network driver?  
    Bridge network.

23. Port mapping command?  
    `docker run -p 80:80 nginx`

24. Host network?  
    Container shares host network.

25. Bridge network?  
    Default isolated network for containers.

### Volumes

26. What is Docker volume?  
    Persistent storage for containers.

27. Create volume?  
    `docker volume create myvol`

28. Mount volume?  
    `docker run -v myvol:/data nginx`

29. Why volumes are used?  
    To store data permanently.

30. Bind mount?  
    Mapping host directory to container.

### Docker Compose

31. What is Docker Compose?  
    Tool to run multi-container applications.

32. Compose file name?  
    `docker-compose.yml`

33. Start compose services?  
    `docker-compose up`

34. Stop compose services?  
    `docker-compose down`

35. Advantage of Docker Compose?  
    Manages multiple containers easily.

### Images

36. List images?  
    `docker images`

37. Tag image?  
    `docker tag image newname`

38. Push image?  
    `docker push repo/image`

39. Docker Hub?  
    Public image repository.

40. Pull latest image?  
    `docker pull nginx:latest`

### Logs & Monitoring

41. View logs?  
    `docker logs container_id`

42. Inspect container?  
    `docker inspect container_id`

43. Container stats?  
    `docker stats`

44. Execute command inside container?  
    `docker exec -it container bash`

45. Pause container?  
    `docker pause container_id`

### Concepts

46. Virtualization vs containerization?  
    Containers share OS kernel; VMs don’t.

47. Lightweight meaning?  
    Uses fewer resources.

48. Immutable image?  
    Image cannot be changed after build.

49. Layered architecture?  
    Images built in layers.

50. Container lifecycle?  
    Create → Run → Stop → Remove.

### Security & Registry

51. What is Docker registry?  
    Storage for Docker images.

52. Private registry?  
    Registry with restricted access.

53. Login Docker Hub?  
    `docker login`

54. Logout Docker Hub?  
    `docker logout`

55. Image scanning?  
    Checks vulnerabilities.

### Build & Run

56. Build without cache?  
    `docker build --no-cache .`

57. Name container?  
    `docker run --name mycontainer nginx`

58. Restart container?  
    `docker restart container_id`

59. Attach container?  
    `docker attach container_id`

60. Detach keys?  
    Ctrl + P + Q

### Environment & Config

61. Set environment variable?  
    `docker run -e VAR=value image`

62. .dockerignore?  
    Excludes files during build.

63. ENTRYPOINT?  
    Defines main container command.

64. EXPOSE?  
    Documents container port.

65. WORKDIR?  
    Sets working directory.

### Cleanup

66. Remove stopped containers?  
    `docker container prune`

67. Remove unused images?  
    `docker image prune`

68. Remove unused volumes?  
    `docker volume prune`

69. System cleanup?  
    `docker system prune`

70. Remove all containers?  
    `docker rm $(docker ps -aq)`

### Advanced Basics

71. Alpine image?  
    Lightweight Linux image.

72. Multi-stage build?  
    Reduces image size.

73. Copy files?  
    `COPY . /app`

74. Add files?  
    `ADD file /app`

75. Difference COPY vs ADD?  
    ADD supports URL and archive extraction.

### Quick Theory

76. Why Docker is used?  
    Consistency across environments.

77. DevOps relation?  
    Used in CI/CD pipelines.

78. Microservices support?  
    Each service runs in container.

79. Scalability?  
    Containers scale easily.

80. Isolation?  
    Apps run independently.

### Final Set

81. Orchestration tool?  
    Kubernetes.

82. Docker Swarm?  
    Docker’s orchestration tool.

83. Container ID?  
    Unique identifier.

84. Image ID?  
    Unique image identifier.

85. Daemon?  
    Background Docker service.

86. CLI?  
    Docker command interface.

87. Namespace?  
    Provides isolation.

88. Cgroups?  
    Resource limits.

89. OverlayFS?  
    Storage driver.

90. OCI?  
    Container standards.

91. Docker Desktop?  
    Docker UI tool.

92. Registry vs repository?  
    Registry stores repos.

93. Latest tag?  
    Default image version.

94. Stateless container?  
    No persistent data.

95. Stateful container?  
    Uses volumes.

96. Container runtime?  
    Runs containers.

97. Image layers cached?  
    Yes.

98. Container port vs host port?  
    Container internal vs host external.

99. Docker open source?  
    Yes.

100. Docker created by?  
     Docker Inc.

---

# Docker INTERMEDIATE Interview Q&A (101–200)

## Image & Build (101–125)

101. What is multi-stage build?  
     A method to create smaller production images using multiple FROM stages.

102. Why multi-stage builds are used?  
     To reduce image size.

103. What is image layer caching?  
     Docker reuses unchanged build layers.

104. How to view image history?  
     `docker history image_name`

105. Difference between CMD and ENTRYPOINT?  
     CMD provides defaults; ENTRYPOINT enforces execution.

106. What is scratch image?  
     An empty base image.

107. What is build context?  
     Directory sent to Docker daemon during build.

108. What is image digest?  
     Unique SHA256 identifier.

109. What is image tagging?  
     Assigning version labels to images.

110. What is docker save?  
     Exports image to tar file.

111. docker load?  
     Imports image from tar file.

112. What is cache busting?  
     Forcing rebuild of layers.

113. What is .dockerignore used for?  
     Exclude files from build context.

114. COPY vs RUN?  
     COPY moves files; RUN executes commands.

115. Docker build argument?  
     `ARG` instruction.

116. ENV instruction?  
     Sets environment variables.

117. LABEL instruction?  
     Adds metadata.

118. ONBUILD instruction?  
     Runs when image is used as base.

119. USER instruction?  
     Specifies container user.

120. HEALTHCHECK?  
     Checks container health.

121. SHELL instruction?  
     Changes default shell.

122. STOPSIGNAL?  
     Defines stop signal.

123. VOLUME instruction?  
     Creates mount point.

124. BuildKit?  
     Improved Docker build system.

125. Inline cache?  
     Cache metadata stored in image.

## Containers & Runtime (126–150)

126. What is container runtime?  
     Software that runs containers.

127. containerd?  
     Docker runtime component.

128. runc?  
     Low-level container runtime.

129. OCI runtime spec?  
     Container runtime standard.

130. What is PID namespace?  
     Process isolation.

131. Mount namespace?  
     Filesystem isolation.

132. Network namespace?  
     Network isolation.

133. IPC namespace?  
     Inter-process communication isolation.

134. UTS namespace?  
     Hostname isolation.

135. User namespace?  
     User isolation.

136. What are cgroups?  
     Resource control mechanism.

137. CPU limit flag?  
     `--cpus`

138. Memory limit flag?  
     `-m`

139. Restart policies?  
     `no`, `always`, `on-failure`, `unless-stopped`.

140. Foreground container?  
     Runs attached to terminal.

141. Detached container?  
     Runs in background.

142. What is TTY?  
     Terminal session.

143. docker attach vs exec?  
     attach connects; exec runs new command.

144. STDIN flag?  
     `-i`

145. Logging drivers?  
     `json-file`, `syslog`, `fluentd`.

146. docker top?  
     Shows processes.

147. docker wait?  
     Waits for container stop.

148. docker rename?  
     Renames container.

149. docker update?  
     Updates resource limits.

150. docker export?  
     Exports container filesystem.

## Networking (151–175)

151. Docker network ls?  
     Lists networks.

152. Create network?  
     `docker network create`

153. Connect container to network?  
     `docker network connect`

154. Disconnect container?  
     `docker network disconnect`

155. Overlay network?  
     Multi-host networking.

156. Macvlan network?  
     Assigns MAC address.

157. None network?  
     No networking.

158. Network inspect?  
     `docker network inspect`

159. DNS in Docker?  
     Embedded DNS server.

160. Container hostname?  
     Container name by default.

161. Link containers?  
     Legacy networking.

162. Network alias?  
     Alternate container name.

163. Custom subnet?  
     User-defined IP range.

164. IPAM?  
     IP address management.

165. Expose vs publish?  
     Expose internal; publish external.

166. Host port binding?  
     Maps host to container.

167. Loopback network?  
     Internal container network.

168. Service discovery?  
     DNS-based container lookup.

169. Bridge driver?  
     Default network driver.

170. Network driver plugin?  
     External network provider.

171. Internal network?  
     No external access.

172. Network gateway?  
     Bridge entry point.

173. Static IP assignment?  
     User-defined network.

174. docker port command?  
     Shows port mapping.

175. IPv6 support?  
     Supported in Docker.

## Volumes & Storage (176–200)

176. Volume driver?  
     Storage backend plugin.

177. Local volume driver?  
     Default driver.

178. tmpfs mount?  
     Memory-based storage.

179. Storage driver?  
     Filesystem backend.

180. overlay2 driver?  
     Default Linux storage driver.

181. aufs driver?  
     Older storage driver.

182. devicemapper?  
     Block-level storage driver.

183. btrfs driver?  
     Filesystem driver.

184. zfs driver?  
     Advanced storage driver.

185. Volume inspect?  
     `docker volume inspect`

186. Anonymous volume?  
     Unnamed volume.

187. Named volume?  
     User-defined volume.

188. Read-only mount?  
     `:ro`

189. Bind mount path?  
     Host directory path.

190. Volume lifecycle?  
     Independent of container.

191. Data persistence?  
     Stored in volumes.

192. Shared volume?  
     Used by multiple containers.

193. Mount propagation?  
     Shared mount behavior.

194. Backup volume?  
     Using tar container.

195. Restore volume?  
     Extract backup archive.

196. Volume pruning?  
     Remove unused volumes.

197. Volume plugin?  
     External storage integration.

198. NFS volume?  
     Network file storage.

199. CIFS volume?  
     Windows file share.

200. Cloud volume integration?  
     Supported via plugins.

---

# Docker ADVANCED Interview Q&A (201–300)

## Architecture (201–230)

201. Docker client?  
     CLI interface.

202. Docker daemon?  
     Background service.

203. REST API?  
     Client-daemon communication.

204. containerd role?  
     Manages container lifecycle.

205. shim process?  
     Keeps container running.

206. OCI image spec?  
     Image format standard.

207. Registry API?  
     Image distribution protocol.

208. Rootless Docker?  
     Run Docker without root.

209. Daemon.json?  
     Docker config file.

210. Live restore?  
     Containers survive daemon restart.

211. Namespaces role?  
     Isolation.

212. Control groups role?  
     Resource limits.

213. Union filesystem?  
     Layered filesystem.

214. Layer reuse?  
     Improves performance.

215. Immutable infrastructure?  
     Replace not modify.

216. Image manifest?  
     Image metadata.

217. Content-addressable storage?  
     Hash-based layers.

218. Pull by digest?  
     Exact image version.

219. Daemon socket?  
     `/var/run/docker.sock`

220. Plugin system?  
     Extends Docker.

221. Secret management?  
     Secure runtime secrets.

222. Config objects?  
     Runtime configuration.

223. Swarm mode?  
     Native orchestration.

224. Manager node?  
     Controls cluster.

225. Worker node?  
     Runs tasks.

226. Service object?  
     Defines containers.

227. Task object?  
     Running container unit.

228. Rolling updates?  
     Gradual deployment.

229. Raft consensus?  
     Cluster state management.

230. Ingress network?  
     Load-balanced routing.

## Security (231–260)

231. Docker security model?  
     Kernel isolation.

232. Seccomp?  
     System call filtering.

233. AppArmor?  
     Access control.

234. SELinux?  
     Mandatory access control.

235. Capabilities?  
     Linux privilege control.

236. Non-root container?  
     Security best practice.

237. Read-only filesystem?  
     Prevent modification.

238. Image signing?  
     Trust verification.

239. Docker Content Trust?  
     Image validation.

240. Notary?  
     Signing service.

241. Secrets in Swarm?  
     Encrypted storage.

242. TLS daemon security?  
     Secure communication.

243. Registry authentication?  
     Access control.

244. Namespace isolation security?  
     Process isolation.

245. Limit container privileges?  
     Drop capabilities.

246. User namespace remap?  
     UID mapping.

247. Scan images?  
     Vulnerability detection.

248. Minimal base images?  
     Reduce attack surface.

249. Avoid latest tag?  
     Version control.

250. Immutable containers?  
     Security consistency.

251. Host isolation risk?  
     Shared kernel.

252. Volume security?  
     Protect host files.

253. Docker socket risk?  
     Root access exposure.

254. Network isolation security?  
     Container firewalling.

255. Resource limits security?  
     Prevent abuse.

256. Logging security?  
     Audit tracking.

257. Registry TLS?  
     Secure transport.

258. Rootless containers?  
     Reduced privilege.

259. Secrets vs ENV?  
     Secrets more secure.

260. Runtime security tools?  
     Falco, etc.

## Performance & Optimization (261–300)

261. Small image strategy?  
     Alpine base.

262. Layer optimization?  
     Combine RUN commands.

263. Cache ordering?  
     Stable layers first.

264. Multi-stage builds benefit?  
     Smaller images.

265. Remove package cache?  
     Reduce size.

266. Limit container CPU?  
     Prevent overload.

267. Limit memory?  
     Prevent OOM.

268. Logging optimization?  
     Use drivers.

269. Volume vs bind mount performance?  
     Volume faster.

270. OverlayFS performance?  
     Efficient layering.

271. Parallel builds?  
     BuildKit feature.

272. Lazy pulling?  
     Partial image download.

273. Registry mirror?  
     Faster pulls.

274. Compression layers?  
     Reduced transfer.

275. Healthchecks?  
     Reliability improvement.

276. Restart policy?  
     High availability.

277. Daemon resource tuning?  
     Performance tuning.

278. Swarm scaling?  
     Horizontal scaling.

279. Container density?  
     Many containers per host.

280. Kernel dependency?  
     Performance factor.

281. I/O limits?  
     Block device control.

282. CPU shares?  
     Relative priority.

283. OOM killer?  
     Memory protection.

284. Container metrics?  
     `docker stats`

285. Monitoring tools?  
     Prometheus.

286. Logging tools?  
     ELK stack.

287. Build cache export?  
     Faster builds.

288. Registry caching?  
     Speeds CI.

289. Immutable images?  
     Deployment reliability.

290. Container startup time?  
     Very fast.

291. Image pre-pulling?  
     Faster deployment.

292. Resource isolation performance?  
     Stable apps.

293. Compose scaling?  
     `--scale`

294. Swarm service scale?  
     `docker service scale`

295. Rolling update delay?  
     Controlled deployment.

296. Node resource labeling?  
     Scheduling control.

297. Health status?  
     `healthy` / `unhealthy`

298. Watchtower?  
     Auto updates.

299. Registry GC?  
     Storage cleanup.

300. Docker best practice?  
     One process per container.

---

# Docker Scenario-Based Interview Questions (300+)

I’ll group them by topic so they’re easier to study.

## Container Issues (1–60)

1. Container exits immediately after start.  
   Check CMD/ENTRYPOINT and logs.

2. Container stuck in restarting state.  
   Check restart policy and logs.

3. Cannot stop container.  
   Use `docker kill`.

4. Container name conflict.  
   Rename or remove existing container.

5. Container not listed in `docker ps`.  
   Use `docker ps -a`.

6. Container crashes on startup.  
   Check logs.

7. Container running but app not responding.  
   Check port mapping.

8. Wrong command executed in container.  
   Verify CMD instruction.

9. Container runs as root unintentionally.  
   Use USER instruction.

10. Cannot attach to container.  
    Ensure container is running.

11. Container consumes high CPU.  
    Check `docker stats`.

12. Container memory issue.  
    Set memory limits.

13. Container cannot access environment variable.  
    Check `-e` flag.

14. Interactive shell not opening.  
    Use `-it`.

15. File not found in container.  
    Check COPY path.

16. Container exits with code 137.  
    Memory limit exceeded.

17. Zombie containers remain.  
    Remove with prune.

18. Container restart loop.  
    Fix application crash.

19. Container stuck in created state.  
    Start container manually.

20. Cannot remove running container.  
    Stop first.

21. Container logs empty.  
    Check logging driver.

22. STDOUT not visible.  
    Use `docker logs`.

23. Multiple containers conflict on port.  
    Change host port.

24. Container timezone wrong.  
    Set TZ environment variable.

25. Container hostname wrong.  
    Use `--hostname`.

26. Container cannot resolve DNS.  
    Check network settings.

27. Container not starting after reboot.  
    Set restart policy.

28. Container file permission error.  
    Check USER and `chmod`.

29. Container shell exits immediately.  
    Keep foreground process running.

30. Container ID changes after rebuild.  
    Normal behavior.

31. Container cannot write to directory.  
    Check volume permissions.

32. App port mismatch.  
    Correct EXPOSE and mapping.

33. Container healthcheck fails.  
    Fix endpoint.

34. Container disk full.  
    Prune images/volumes.

35. Container slow startup.  
    Optimize image.

36. Missing dependencies inside container.  
    Install in Dockerfile.

37. Container can't ping internet.  
    Check network.

38. Container environment resets.  
    Use volumes.

39. Container fails after image update.  
    Rollback image.

40. Container stuck stopping.  
    Force kill.

41. Container cannot run script.  
    Make executable.

42. Container loops execution.  
    Check entrypoint script.

43. Container file overwritten.  
    Volume mount issue.

44. Container not using latest image.  
    Pull image again.

45. Container logs too large.  
    Rotate logs.

46. Container user mismatch.  
    Check UID mapping.

47. Container cannot access host file.  
    Use bind mount.

48. Container network unreachable.  
    Restart network.

49. Container cannot start service.  
    Service config issue.

50. Container time drift.  
    Sync host time.

51. Container working locally but not server.  
    Environment mismatch.

52. Container permission denied error.  
    Fix ownership.

53. Container rebuild too slow.  
    Use cache layers.

54. Container command overridden.  
    Check run command.

55. Container exits without logs.  
    Enable logging.

56. Container fails after restart.  
    Check stateful data.

57. Container uses wrong config file.  
    Verify mount path.

58. Container cannot load library.  
    Install dependency.

59. Container cannot write logs.  
    Fix permissions.

60. Container not running as expected.  
    Inspect container.

## Image Build Issues (61–120)

61. Image build fails.  
    Check Dockerfile syntax.

62. Build context too large.  
    Use `.dockerignore`.

63. Image too big.  
    Use Alpine.

64. Build slow.  
    Optimize layers.

65. Cache not used.  
    Layer order changed.

66. RUN command fails.  
    Check command.

67. COPY fails.  
    Wrong path.

68. Base image not found.  
    Check tag.

69. Dockerfile not detected.  
    Check filename.

70. Image build permission error.  
    Check file access.

71. Build network failure.  
    Check internet.

72. ENV variable missing.  
    Define ENV.

73. Image missing binary.  
    Install package.

74. ENTRYPOINT script fails.  
    Check script.

75. Multi-stage build fails.  
    Wrong stage name.

76. Image rebuild always triggered.  
    Changing layers.

77. Image tag overwritten.  
    Use version tags.

78. Image pull denied.  
    Login registry.

79. Private repo access issue.  
    Add credentials.

80. Image corrupted.  
    Rebuild.

81. ADD URL fails.  
    Network issue.

82. CMD ignored.  
    ENTRYPOINT override.

83. Dockerfile variable missing.  
    ARG not defined.

84. Permission denied in RUN.  
    Switch USER.

85. Layer size large.  
    Combine RUN commands.

86. Build fails on CI.  
    Environment mismatch.

87. Package install fails.  
    Repository issue.

88. File copied incorrectly.  
    Wrong path.

89. Build timeout.  
    Network slow.

90. Build fails randomly.  
    Dependency instability.

91. Image registry push fails.  
    Login again.

92. Tag mismatch.  
    Check repo name.

93. Wrong base OS.  
    Change base image.

94. Image vulnerability found.  
    Update packages.

95. Missing WORKDIR.  
    Define working directory.

96. ENTRYPOINT not executable.  
    `chmod +x`.

97. Dockerfile indentation issue.  
    Fix syntax.

98. BuildKit disabled.  
    Enable BuildKit.

99. Image not reproducible.  
    Pin versions.

100. Build fails at final stage.  
     Check dependencies.

(Continuing networking, volumes, compose, swarm, registry, performance…)

To keep this readable, here is the remaining set condensed but still interview-useful.

## Networking Scenarios (121–180)

Common answers:

- Check network  
- Check port mapping  
- Inspect container  
- Restart Docker  
- Verify DNS  
- Verify firewall

Examples:

- Containers cannot communicate → same network  
- Port not accessible → map port  
- DNS fails → check `/etc/resolv.conf`  
- Host cannot access container → publish port  
- Two containers same port → change mapping  
- Overlay network not working → check swarm

## Volume & Storage Scenarios (181–240)

Common answers:

- Check mount path  
- Check permissions  
- Use named volume  
- Inspect volume  
- Verify ownership

Examples:

- Data lost after container restart → use volume  
- Cannot write to volume → fix permissions  
- Volume not mounted → check `-v`  
- Wrong directory mounted → verify path  
- Backup volume fails → tar command fix

## Compose / Swarm / Registry / Performance (241–300)

Common answers:

- Check compose file  
- Validate YAML  
- Check service logs  
- Check registry login  
- Optimize image  
- Scale service

Examples:

- `docker-compose up` fails → validate YAML  
- Service not scaling → check replicas  
- Registry push timeout → network issue  
- Compose env variable missing → `.env` file  
- Deployment slow → pre-pull image

---

# Top 50 Docker Troubleshooting Interview Questions

## Container Startup Issues

1. Container exits immediately after starting. What do you check?  
   Check logs using `docker logs` and verify CMD/ENTRYPOINT.

2. Container is restarting continuously. Why?  
   Application inside container is failing.

3. Container shows "Exited (137)". What does it mean?  
   Container was killed due to memory limit.

4. Container is created but not running.  
   Start it using `docker start`.

5. Application runs locally but not inside Docker.  
   Dependency or environment issue.

## Logs & Debugging

6. How do you debug a failing container?  
   Check logs and exec into container.

7. Command to view logs?  
   `docker logs container_id`

8. Enter running container?  
   `docker exec -it container bash`

9. Inspect container configuration?  
   `docker inspect`

10. Monitor resource usage?  
    `docker stats`

## Port & Network Problems

11. Container running but website not accessible.  
    Check port mapping.

12. Two containers cannot communicate.  
    Ensure same Docker network.

13. Host cannot access container port.  
    Publish port using `-p`.

14. DNS resolution fails inside container.  
    Check Docker network DNS.

15. Port already in use error.  
    Use different host port.

## Image Build Problems

16. Docker build fails.  
    Check Dockerfile syntax.

17. COPY instruction not working.  
    Check file path.

18. RUN command failing during build.  
    Verify package install command.

19. Image size too large.  
    Use Alpine base image.

20. Build is very slow.  
    Optimize Dockerfile layers.

## Volume Issues

21. Data lost after container restart.  
    Use volumes.

22. Cannot write to mounted volume.  
    Fix permissions.

23. Volume not mounting correctly.  
    Check mount path.

24. File missing in container.  
    Verify bind mount.

25. Container overwriting host files.  
    Mount path issue.

## Registry & Image Issues

26. Cannot pull image from Docker Hub.  
    Check internet or login.

27. Push to registry fails.  
    Run `docker login`.

28. Wrong image version deployed.  
    Check image tag.

29. Latest image not pulled.  
    Use `docker pull`.

30. Private registry access denied.  
    Authentication issue.

## Resource & Performance Issues

31. Container using high CPU.  
    Check with `docker stats`.

32. Container memory issue.  
    Set memory limits.

33. Disk space full due to Docker.  
    Run `docker system prune`.

34. Too many unused images.  
    Remove with `docker image prune`.

35. Slow container startup.  
    Optimize image size.

## Permission & Security Issues

36. Permission denied error in container.  
    Check file ownership.

37. Container running as root.  
    Use USER instruction.

38. Cannot execute script in container.  
    Add executable permission.

39. Host file access denied.  
    Fix mount permissions.

40. Docker socket permission issue.  
    Add user to docker group.

## Docker Compose Issues

41. `docker-compose up` fails.  
    Check YAML syntax.

42. Environment variables not loading.  
    Check `.env` file.

43. Service not accessible in compose.  
    Check ports section.

44. Compose service not restarting.  
    Add restart policy.

45. Container name conflict in compose.  
    Remove existing container.

## Common Real Interview Debug Questions

46. How do you clean unused Docker resources?  
    `docker system prune`

47. How do you remove all stopped containers?  
    `docker container prune`

48. How do you remove dangling images?  
    `docker image prune`

49. How do you check Docker daemon status?  
    `systemctl status docker`

50. How do you restart Docker service?  
    `systemctl restart docker`

# Docker Interview Questions — Extended Set

This file contains grouped Docker interview questions covering Dockerfile & image building, commands & container management, networking, volumes, Compose, and troubleshooting. Use this as a study sheet or convert it into flashcards.

---

## Dockerfile & Image Building (1–50)

1. What is a Dockerfile?  
2. What does FROM instruction do?  
3. Difference between CMD and ENTRYPOINT?  
4. What is RUN instruction?  
5. COPY vs ADD?  
6. What is WORKDIR?  
7. What is ENV?  
8. What is ARG?  
9. What is multi-stage build?  
10. Why use Alpine images?  
11. What are Docker image layers?  
12. How does layer caching work?  
13. How to reduce image size?  
14. What is base image?  
15. What is image tag?  
16. What is docker build?  
17. What is build context?  
18. What is .dockerignore?  
19. What is image digest?  
20. What is docker history?  
21. What is docker save?  
22. What is docker load?  
23. What is HEALTHCHECK?  
24. What is LABEL?  
25. What is USER instruction?  
26. What is VOLUME instruction?  
27. What is EXPOSE instruction?  
28. What is ENTRYPOINT script?  
29. What is ONBUILD?  
30. What is scratch image?  
31. What is immutable image?  
32. How to optimize RUN commands?  
33. What is BuildKit?  
34. How to rebuild without cache?  
35. What is image registry?  
36. How to tag image?  
37. How to push image?  
38. What is docker commit?  
39. What is image manifest?  
40. What is container filesystem layer?  
41. Why combine RUN commands?  
42. What is dependency installation layer?  
43. What is build argument usage?  
44. What is shell form vs exec form?  
45. What is image reproducibility?  
46. What is container image scanning?  
47. What is docker export?  
48. What is docker import?  
49. What is ENTRYPOINT override?  
50. Why is Dockerfile order important?

---

## Docker Commands & Container Management (51–100)

51. What does docker run do?  
52. What is docker ps?  
53. What is docker stop?  
54. What is docker start?  
55. What is docker rm?  
56. What is docker exec?  
57. What is docker logs?  
58. What is docker inspect?  
59. What is docker stats?  
60. What is docker top?  
61. What is docker kill?  
62. What is docker restart?  
63. What is docker attach?  
64. What is docker pause?  
65. What is docker unpause?  
66. What is container ID?  
67. What is container name?  
68. What is detached mode?  
69. What is interactive mode?  
70. What is STDIN flag?  
71. What is restart policy?  
72. What is --name flag?  
73. What is port mapping?  
74. What is environment variable flag?  
75. What is container lifecycle?  
76. What is docker rename?  
77. What is docker wait?  
78. What is docker cp?  
79. What is docker diff?  
80. What is docker update?  
81. What is foreground container?  
82. What is background container?  
83. What is container logging?  
84. What is container health status?  
85. What is docker system prune?  
86. What is docker image prune?  
87. What is docker container prune?  
88. What is container exit code?  
89. What is PID 1 process?  
90. What is TTY?  
91. What is Docker CLI?  
92. What is daemon communication?  
93. What is container runtime?  
94. What is docker version?  
95. What is docker info?  
96. What is container metadata?  
97. What is container configuration?  
98. What is container isolation?  
99. What is command override?  
100. What is container execution mode?

---

## Docker Networking (101–150)

101. What is Docker networking?  
102. What is bridge network?  
103. What is host network?  
104. What is overlay network?  
105. What is none network?  
106. What is port publishing?  
107. What is container IP?  
108. What is DNS inside Docker?  
109. What is network namespace?  
110. What is network driver?  
111. What is docker network create?  
112. What is docker network ls?  
113. What is docker network inspect?  
114. What is docker network connect?  
115. What is docker network disconnect?  
116. What is service discovery?  
117. What is container hostname?  
118. What is network alias?  
119. What is gateway?  
120. What is subnet?  
121. What is IPAM?  
122. What is static container IP?  
123. What is loopback network?  
124. What is container communication?  
125. What is firewall interaction?  
126. What is NAT in Docker?  
127. What is port binding?  
128. What is internal network?  
129. What is external network?  
130. What is network isolation?  
131. What is DNS resolution?  
132. What is multi-host networking?  
133. What is ingress network?  
134. What is container port vs host port?  
135. What is IPv6 support?  
136. What is network plugin?  
137. What is load balancing in Docker?  
138. What is overlay encryption?  
139. What is bridge gateway?  
140. What is container routing?  
141. What is network attachable?  
142. What is container endpoint?  
143. What is network scope?  
144. What is MAC address assignment?  
145. What is container link?  
146. What is network stack?  
147. What is port exposure?  
148. What is network latency?  
149. What is DNS caching?  
150. What is network configuration?

---

## Docker Volumes (151–200)

151. What is Docker volume?  
152. What is bind mount?  
153. What is tmpfs mount?  
154. What is volume driver?  
155. What is local volume?  
156. What is named volume?  
157. What is anonymous volume?  
158. What is volume lifecycle?  
159. What is data persistence?  
160. What is mount point?  
161. What is docker volume create?  
162. What is docker volume ls?  
163. What is docker volume inspect?  
164. What is docker volume rm?  
165. What is volume pruning?  
166. What is read-only mount?  
167. What is shared volume?  
168. What is storage driver?  
169. What is overlay2?  
170. What is filesystem isolation?  
171. What is mount propagation?  
172. What is volume backup?  
173. What is volume restore?  
174. What is NFS volume?  
175. What is CIFS volume?  
176. What is cloud volume plugin?  
177. What is container writable layer?  
178. What is host path mount?  
179. What is data integrity?  
180. What is volume security?  
181. What is mount permission?  
182. What is storage backend?  
183. What is volume metadata?  
184. What is volume container?  
185. What is Docker storage architecture?  
186. What is disk usage monitoring?  
187. What is storage cleanup?  
188. What is container storage limit?  
189. What is snapshot backup?  
190. What is file locking?  
191. What is shared filesystem?  
192. What is persistent service data?  
193. What is mount consistency?  
194. What is filesystem driver?  
195. What is data synchronization?  
196. What is storage performance?  
197. What is volume isolation?  
198. What is distributed storage?  
199. What is backup automation?  
200. What is storage scaling?

---

## Docker Compose (201–250)

201. What is Docker Compose?  
202. What is docker-compose.yml?  
203. What is service in Compose?  
204. What is compose network?  
205. What is compose volume?  
206. What is compose build?  
207. What is compose image?  
208. What is compose environment?  
209. What is compose ports?  
210. What is compose depends_on?  
211. What is docker-compose up?  
212. What is docker-compose down?  
213. What is docker-compose build?  
214. What is docker-compose logs?  
215. What is docker-compose ps?  
216. What is compose scaling?  
217. What is compose restart?  
218. What is compose config?  
219. What is compose override file?  
220. What is compose project name?  
221. What is compose profiles?  
222. What is compose secrets?  
223. What is compose configs?  
224. What is compose healthcheck?  
225. What is compose restart policy?  
226. What is compose network driver?  
227. What is compose external network?  
228. What is compose external volume?  
229. What is compose build context?  
230. What is compose command override?  
231. What is compose entrypoint override?  
232. What is compose logging?  
233. What is compose container naming?  
234. What is compose variable substitution?  
235. What is compose extension field?  
236. What is compose lifecycle?  
237. What is compose dependency order?  
238. What is compose multi-container app?  
239. What is compose development workflow?  
240. What is compose production config?  
241. What is compose service discovery?  
242. What is compose port mapping?  
243. What is compose volume mount?  
244. What is compose network isolation?  
245. What is compose environment file?  
246. What is compose build cache?  
247. What is compose container recreation?  
248. What is compose resource limits?  
249. What is compose scaling command?  
250. What is compose deployment?

---

## Docker Troubleshooting (251–300)

251. Container not starting — what to check?  
252. Container exits immediately — why?  
253. Port not accessible — what to verify?  
254. Volume not persisting — why?  
255. Image build failing — first step?  
256. Permission denied inside container — cause?  
257. Cannot pull image — reason?  
258. Cannot push image — reason?  
259. Container restarting repeatedly — cause?  
260. Logs not showing — why?  
261. Docker daemon not running — fix?  
262. Disk space full — solution?  
263. High CPU container — check?  
264. Memory issue container — fix?  
265. Container cannot reach internet — why?  
266. Two containers cannot communicate — why?  
267. DNS failure in container — fix?  
268. Compose service not starting — check?  
269. YAML syntax error — fix?  
270. Container name conflict — fix?  
271. Image outdated — solution?  
272. Dockerfile build slow — fix?  
273. Build cache not used — why?  
274. ENTRYPOINT failing — check?  
275. CMD ignored — why?  
276. Bind mount not working — why?  
277. Volume permission error — fix?  
278. Docker login fails — why?  
279. Registry timeout — cause?  
280. Container healthcheck failing — why?  
281. Container logs too large — fix?  
282. Container stuck stopping — fix?  
283. Docker network missing — fix?  
284. Compose env variable missing — fix?  
285. Service dependency issue — fix?  
286. Container cannot write file — fix?  
287. Host file not visible — why?  
288. Container timezone wrong — fix?  
289. Restart policy not working — why?  
290. Container resource limit ignored — why?  
291. Container process not visible — why?  
292. Docker service crash — recovery?  
293. Overlay network not working — cause?  
294. Image push permission denied — why?  
295. Docker CLI not responding — fix?  
296. Container exec fails — why?  
297. Container IP changed — why?  
298. Docker update fails — why?  
299. Compose rebuild required — when?  
300. Docker environment mismatch — fix?

---
