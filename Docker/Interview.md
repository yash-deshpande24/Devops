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
