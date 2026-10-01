* DESIGN
	* Web user: [Figma](https://www.figma.com/design/JMguT903F9gGTw3Z63J5T2/Procuro?node-id=1986-17089&m=dev)
	* Admin: [Figma](https://www.figma.com/design/Wg2yGfkk9uOBZRfb1S3Nfm/Biz-Projects?node-id=0-1&p=f&t=vjrYwZSbIoDjc5oC-0)

* SPEC
	* Web user:
		* Lastest: 
		* Old version: 
	* Admin
		* Lastest: [Lark](https://ujbc4oj6ouc.sg.larksuite.com/docx/K967dPp33odHnUxYIPqluUmxgih)
		* Old version:

* TEST [Excel](https://docs.google.com/spreadsheets/d/1j6VGAcnI0JYbeYwrsBcRB0u6UXcnLOvtaI6m5I0hNaU/edit?gid=776750613#gid=776750613)

* SOURCE CODE: [GIT](https://github.com/APECGROUP/Fourier.Procuro)

* DEPLOY
	* Môi trường test: 
		* Admin: https://procuro-cms-test.fourier.group/
		* Web user: https://procuro-test.fourier.group
	 * Môi trường Production:
		 * Admin: https://procuro-cms.mhgglobalhotel.com/dashboard
			 * tk: admin@procuro.vn
			 * mk: 123456aA@
		 * Web user: https://procuro.mhgglobalhotel.com/





## TECHICAL

| Layer         | Stack                                                                                                                                                                          |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Backend       | NestJS + Prisma + Postgres, Clean Architecture, `nestjs-pino` logging                                                                                                          |
| Requester app | Next.js + **Tailwind CSS**                                                                                                                                                     |
| Admin app     | Vite + Refine + Ant Design                                                                                                                                                     |
| Monorepo      | Nx + **pnpm**                                                                                                                                                                  |
| Testing       | Jest (backend unit + e2e), Vitest (FE unit), Playwright (FE e2e)                                                                                                               |
| Build/Deploy  | Docker multi-stage (mirror `Dockerfile.api`/`Dockerfile.cms`), docker-compose, CI/CD dùng chung hạ tầng APEC (registry, ArgoCD, `apec-deploy-manifest`)                        |
| Code sync     | ESLint+Prettier+Nx module boundaries, husky+lint-staged+commitlint, Conventional Commits, Nx generator riêng cho module backend, format enforce qua `nx format:check` trong CI |
| Auth          | JWT tự xây, role: REQUESTER / APPROVER / ADMIN        

