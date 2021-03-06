DRUPAL 8
========

#### Consultas mediante sql
```
//múltiples filas
$result = db_query('SELECT id, qualifier, email, board, popup
          FROM {k_message}
          WHERE rule = :rid',
          array(':rid' => $idRule)
);

foreach ($result as $record) {
  $idMessage = $record->id;
  $qualifier = $record->qualifier;
  $emailMsg = $record->email;
  $boardMsg = $record->board;
  $popupMsg = $record->popup;
}
 
//optener valor de un sólo campo
$addFactor =  db_query('SELECT value FROM k_factor WHERE id = :id;', array(':id' => $id))->fetchField();
```

#### Consultas mediante Entidades

```
//crear entidad
$voucher =  array(
  'iden' => $_SESSION['entity']['id'],
  'idam' => 1, //to do: set dinamic this value
  'number' => NUll, //entity has a presave()
  'date' => $form_state->getValue('date'),
  'description' => $form_state->getValue('gloss'),
  'type' => $form_state->getValue('type'),
  'subtype' => NULL,
  'amount' => NULL,
  'state' => "REGISTERED",
  'userid' => \Drupal::currentUser()->id(),
);
      
$entityVoucher = entity_create('k_voucher', $voucher);
$entityVoucher->Save();
$idVoucher = $entityVoucher->id();

//obtener una entidad mediante consulta
$idsAccountPlan = \Drupal::entityQuery('k_accountplan')
->condition('iden', $entity, '=')
->condition('idac', $account->getIdac(), '=')
->condition('idam', $accountingManagement, '=')
->execute();
$accountPlan = AccountPlan::load(reset($idsAccountPlan));

//obtener multiples entidades mediante consulta
$idsEntries = \Drupal::entityQuery('k_accountingentry')
->condition('idvo', $voucher->getIdvo(), '=')
->execute();
$entries = AccountingEntry::loadMultiple($idsEntries);
foreach ($entries as $entrie) {
 ... hacer algo con las entidades ...
}
      
//obtener datos de entidades foraneas
$entity->idac->target_id;
$entity->idac->entity->label();
      
//obtner valor de un atributo de la entidad
$rule->get('variable')->value
```

#### Formularios

```
//Obtener todos los elementos de un form_state
foreach ($form_state->getValues() as $key => $value) {
      drupal_set_message($key . ': ' . $value);
}
//Obtener un elemento de un form_state
$searched = $form_state->getValue('nombre_elemento_formulario');
    
```
#### Sentencias usuales

```
//Guardar un texti en el log (Watchdog)
\Drupal::logger('mi_modulo')->notice(Mi mensaje");
\Drupal::logger('mi_modulo')->error("Mi mensaje");

//Acceder a las configuraciones del cron
\Drupal::config('system.cron')->get('threshold.autorun')
\Drupal::state()->get('system.cron_last')

//Mensajes del sistema
drupal_set_message("Mi mensaje");
```

### Seguridad
```
Permisos
sites -> 755
sites/default -> 755
sites/default/files -> 775
sites/default/settings.php -> 444
sites/default/services.yml -> 444
```

ENLACES Y FUENTES
=================
Documentación oficial
https://api.drupal.org/api/drupal/8

Documentación de la comunidad
https://www.drupal.org/developing/api/8

Clases de drupal 8
https://api.drupal.org/api/drupal/classes/8

Hoja resumida de codigo
http://wizzlern.nl/sites/wizzlern.nl/files/artikel/drupal8_content_entity.pdf

Watchdow drupal 8
https://www.drupal.org/node/2270941
