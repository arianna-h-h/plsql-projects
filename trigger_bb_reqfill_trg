create or replace trigger bb_reqfill_trg
   AFTER UPDATE OF DTRECD ON bb_product_request
   for each row
DECLARE
  v_stock bb_product_request.qty%type;
  v_id bb_product_request.idproduct%type;
 BEGIN
   If :OLD.DTRECD is not null and :NEW.DTRECD is null THEN
    Update BB_PRODUCT
    set stock = stock - reorder
     WHERE idProduct = :NEW.idProduct;
    elsif :NEW.DTRECD is not null THEN
    Update BB_PRODUCT
    set stock = reorder + stock
     WHERE idProduct = :NEW.idProduct;
    end if;
       end;
