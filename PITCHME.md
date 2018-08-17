# Devops #

Um overview sobre as soluções adotadas e a forma de criação do ambiente.

---

## Arquitetura ##

A ideia era um ambiente simples:

- Dois ambientes de execução:
  - `Blue`
  - `Green`
- Cada ambiente em mais de uma AZ
  - `A`
  - `C`

---?image=assets/images/architecture_diagram.jpg&size=auto 80%&opacity=100

---

@title[Tentativa inicial]

```
resource "aws_instance" "adesao_spring_boot" {
  ami                     = "${data.aws_ami.amazon_linux.id}"
  instance_type           = "${var.instance_type}"
  iam_instance_profile    = "${data.aws_iam_role.oicontrole.name}"
  user_data               = "${data.template_file.blue.rendered}"
  disable_api_termination = "${var.termination_protection}"
  key_name                = "${var.key_name}"
  subnet_id               = "${aws_subnet.subnet_adesao_spring.id}"
  vpc_security_group_ids = [
    ...
  ]
  tags {
    ...
  }
}
```

---

![Flux Explained](https://facebook.github.io/flux/img/flux-simple-f8-diagram-explained-1300w.png)
