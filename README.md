# Ansible Windows and Linux Administration Playbooks

Repozytorium prezentuje praktyczne playbooki Ansible do automatyzacji zadań administracyjnych na serwerach Windows, stacjach Windows i hostach Linux.

## Co pokazuje repozytorium

- automatyzację administracji Windows przez WinRM,
- użycie kolekcji `ansible.windows`,
- zadania serwisowe dla RDS/Print Spooler,
- diagnostykę wersji systemów i łączności,
- przykład naprawy ustawień Windows Update,
- podejście bez sekretów i bez produkcyjnych hostów w repozytorium.

## Struktura

| Katalog | Playbook | Zakres |
|---|---|---|
| `windows/` | `check-os-version-windows-servers.yml` | Pobranie wersji systemu Windows z serwerów. |
| `windows/` | `ping-windows-servers.yml` | Test połączenia WinRM z serwerami Windows. |
| `windows/` | `ping-windows-workstations.yml` | Test połączenia WinRM ze stacjami roboczymi. |
| `windows/` | `repair-windows-update-policy.yml` | Usunięcie problematycznych polityk Windows Update i restart usługi. |
| `rds/` | `rds-print-spooler-maintenance.yml` | Uruchomienie bufora wydruku, czyszczenie kolejki i powiadomienie. |
| `software/` | `find-installed-exampleapp.yml` | Wyszukiwanie przykładowej aplikacji w rejestrze Windows. |
| `software/` | `uninstall-exampleapp.yml` | Odinstalowanie przykładowej aplikacji. |
| `linux/` | `check-os-version-linux.yml` | Pobranie dystrybucji i wersji systemów Linux. |

## Szybki start

1. Skopiuj przykładowy inventory:

```bash
cp inventory.example.ini inventory.ini
```

2. Uzupełnij hosty i poświadczenia. Hasła przechowuj w Ansible Vault albo podawaj bezpiecznie w runtime.

3. Uruchom playbook:

```bash
ansible-playbook -i inventory.ini windows/ping-windows-servers.yml
ansible-playbook -i inventory.ini windows/check-os-version-windows-servers.yml
```

## Webhooki i sekrety

Webhook Discord jest przekazywany jako zmienna, a nie hardkodowany w repozytorium:

```bash
ansible-playbook -i inventory.ini rds/rds-print-spooler-maintenance.yml   -e "discord_webhook_url=$DISCORD_WEBHOOK_URL"
```

Nie commituj plików `inventory.ini`, `vault.yml`, `.env` ani realnych tokenów.

## Wymagania

- Ansible na hoście kontrolnym,
- kolekcja `ansible.windows`,
- skonfigurowany WinRM dla hostów Windows,
- konto z uprawnieniami administracyjnymi do wykonywanych operacji,
- Ansible Vault lub inny bezpieczny mechanizm na poświadczenia.

## Bezpieczeństwo

Repozytorium jest przygotowane jako portfolio. Nazwy hostów, grup i aplikacji są przykładowe, a sekrety należy przekazywać poza repozytorium.
