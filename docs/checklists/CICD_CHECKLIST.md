# Checklist de CI/CD

- [ ] Pipeline `.gitlab-ci.yml` versionada no repositório
- [ ] Stages de validação, teste, build e deploy definidas
- [ ] Build separado por componente ou stack
- [ ] Publicação em Harbor documentada
- [ ] GitLab Runner de build documentado
- [ ] GitLab Runner de deploy documentado
- [ ] Variáveis obrigatórias de CI/CD documentadas
- [ ] Deploy por ambiente documentado
- [ ] Tags de imagem por branch e commit documentadas
- [ ] Rollback por versão ou tag documentado
- [ ] Migrations integradas ao fluxo quando aplicável
- [ ] Logs de deploy e troubleshooting documentados
- [ ] Produção não depende de compose único
